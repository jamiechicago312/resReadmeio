---
title: "Reservoir Sync Node"
slug: "reservoir-sync-node"
excerpt: "A customizable lightweight indexer based on the Reservoir indexer. Continuously sync sales, transfers, asks, and bids into your infrastructure."
hidden: false
createdAt: "2023-07-26T18:16:00.662Z"
updatedAt: "2023-08-07T19:29:22.533Z"
---
## Introduction

The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node) provides an easy-to-launch syncing system to keep up to date and retrieve bulk NFT data from the Reservoir Data Lake. Currently, our sync node supports backfilling & live syncing for  [bids](https://docs.reservoir.tools/docs/syncing-bids), [asks](https://docs.reservoir.tools/docs/syncing-asks) and [sales ](https://docs.reservoir.tools/docs/syncing-sales), and [transfers](https://docs.reservoir.tools/reference/gettransfersv3) data.  We highly recommend utilizing the sync node when it comes to handling the task of backfilling historical data. Current backfill time is about 1 Hour for about 8 to 10 million rows of data. This methodology provides a streamlined way to manage large datasets effectively, while also reducing time & API usage.

### Architecture

The Reservoir Sync Node employs a methodology known as "graining," designed to handle larger datasets by partitioning them into smaller, manageable chunks. This technique involves sequentially dividing a larger time span into more compact blocks, which are then processed in parallel to optimize efficiency and performance.

Initially, the system operates on a broad date range. It then continuously segments this range into smaller intervals or 'blocks.' The determination of these splits is guided by the data density within the blocks.

Graining progresses until blocks reach a point where the timestamp difference, representing the data's temporal span, is less than 10 minutes. This condition implies that each resulting block encompasses 10 minutes' worth of data. This process is iterated until all blocks are equal to or smaller than 10 minutes in size. **10 Minutes was the size that we determined based on the overall density of our database. This 10 minute block size allowed for the most efficient sync speed.** This can be modified accordingly on your own fork to either be higher, or lower.

After completion of the graining process, these blocks are ready for processing. The system employs continuation pagination tokens to retrieve all records within each block. This approach ensures that all data within these time-constrained blocks is efficiently accessed and processed.

### Installation

> 🚧 Migration of SyncNode V1 to V2
> 
> As of July 28th, an extensive architectural upgrade has been made to the SyncNode. This update, which we refer to as V2, substantially improves both syncing speed and resource usage, marking a large performance increase over V1. However, due to the many changes in this update, some aspects need to be noted and reconfigured for those migrating from V1. **If you are just getting started with the SyncNode, feel free to skip over this and head straight to Installation below**
> 
> Transitioning to V2 is a straightforward process. Please observe the following changes and adhere to the guide provided to ensure a seamless migration:
> 
> 1. A big aspect of SyncNode V2 is its utilization of two distinct processes. This is important as some system providers only permit a single process to be spawned in a given environment. You can refer to these as the "Sync" process and "Server Process". This was done to decrease overall memory usage on the "Sync" process. 
> 
> 2. The `CONTRACTS=` environment variable previously used has been phased out. Instead, we've introduced a `contracts.txt` file. This will now serve as the primary means of managing your contracts, providing a more straightforward and intuitive approach.
> 
> 3. The `WORKERS_COUNT=` and `MANAGER_COUNT=` environment variables have been eliminated. In the past, these variables introduced complex terms that relied on understanding the system's inner workings, in order to be best configured. To simplify this, we've replaced them with a `MODE=` variable. This can be configured to `fast`, `normal`, or `slow`, allowing for more user-friendly, high-level control over system performance. See the metrics below for how each mode performs.
> 
> 4. Previously the SyncNode stored the block queue in memory. For better performance we have migrated it over to redis. In order to avoid complications while booting up the node, ensure that you have flushed the redis database using the `yarn purge:backup`.

To install the required dependencies for the Light Sync Node, run:

```bash
yarn installl
```

### Configuration - ENV

Included is an example .env file (example.env). Rename it to .env and configure as shown below:

### SyncNode ENV

```
# ====================
# Server Configuration
# ====================

# PORT (Required): The port on which the server should run
PORT=

# AUTHORIZATION (Required): The server authorization string
AUTHORIZATION=

# ====================
# Logger Configuration
# ====================

# DATADOG_APP_NAME (Optional): The name of the Datadog app for sending internal logs
#DATADOG_APP_NAME=

# DATADOG_API_KEY (Optional): The API key for the above Datadog app
#DATADOG_API_KEY=

# ========================
# Database Configuration
# ========================

# DATABASE_URL (Required): The URL of the Postgres database
DATABASE_URL=

# REDIS_URL (Required): Redis URL for storing the active queues and backups
REDIS_URL=

# ====================
# Syncer Configuration
# ====================

# CHAIN (Required): The chain to sync. Supported chains: 'mainnet', 'goerli', 'polygon', 'arbitrum' 'optimism'
CHAIN=

# API_KEY (Required): Reservoir API key. Sign up for free at https://reservoir.tools/
API_KEY=

# SYNC_SALES (Optional): Enable syncing/backfilling of sales (1 = TRUE, 0 = FALSE)
SYNC_SALES=

# SYNC_ASKS (Optional): Enable syncing/backfilling of asks (1 = TRUE, 0 = FALSE)
SYNC_ASKS=

# SYNC_BIDS (Optional): Enable syncing/backfilling of bids (1 = TRUE, 0 = FALSE)
SYNC_BIDS=

# SYNC_TRANSFERS (Optional): Enable syncing/backfilling of bids (1 = TRUE, 0 = FALSE)
SYNC_TRANSFERS=
  
# MODE (Required): Speed of the SyncNode. Options: 'slow', 'normal', 'fast'
MODE=

# USE_BACKUP (Optional): Enable usage of the backup stored in Redis (1 = TRUE, 0 = FALSE). If 0, the backup is flushed.
USE_BACKUP=
```

You will also need to configure an env for the viewer which is shown below

### Viewer ENV

```
# Domain that application is deployed on
REACT_APP_SERVER_DOMAIN=
```

### Configuration - (Prisma) Database

[Prisma ORM](https://www.prisma.io) is used to interact with a PostgresSQL datbase.  
To configure please setup the `.env` as shown below: 

```env
DATABASE_URL=your-postgres-database-url
```

> 🚧 For Users Integrating with an Existing or Populated Database
> 
> If you're setting up your SyncNode with a database that already contains tables, please execute the following command **before** proceeding.
> 
> **Please make sure you've backed up your data before moving forward. While _this command should not wipe data_ it is best that you take precautions to ensure a smooth configuration.**
> 
> Run: `yarn database:introspect`
> 
> This command executes two tasks:
> 
> 1. It triggers the script `node ./scripts/database-apply.js`, which executes SQL using the `prisma.executeRaw` method, to create the required tables (asks, sales, bids). This is manually done as to avoid introspecting your entire database into the schema.prisma file.
> 2. It triggers the script `npx prisma migrate resolve --applied sync_node_migration` to form a baseline of migration history in your database. This baseline is required since Prisma needs to confirm that your database schema is in sync with your schema model. For a comprehensive understanding, please refer to the Prisma documentation on [baselining](https://www.prisma.io/docs/guides/migrate/developing-with-prisma-migrate/baselining).
> 
> Bear in mind that, due to Prisma's specific requirements, a Prisma migration table must be applied to your database to establish the migration history baseline. This migration table reassures the Prisma client that your database tables are accurately mirrored in the schema.prisma file.

For further assistance setting up Prisma please visit their [documentation](https://www.prisma.io/docs).

### Configuration - (Redis) Backups

[Redis](https://www.redis.com) is used to store temporary backups of the current state of the Sync Node in case it is to go down.  
This allows the Sync Node to restart right where it left off.  
For easy an easy no hassle setup use: <https://redis.com/try-free>.

To configure please setup the `.env` as shown below: 

```env
REDIS_URL=your-redis-url
```

### Usage

To launch the Sync Node, run the command below: 

```
yarn start
```

### Performance Metrics

Below are some metrics that have been gauged on [Railway](https://railway.app). 

These metrics along with your RPS (Requests Per Second) & Total Requests will fluctuate/vary depending on a variety of factors. These metrics were calculated with a single dataset being synced.

| RPS (Requests Per Second)                         | Mode   | Memory Usage (avg) |
| :------------------------------------------------ | :----- | :----------------- |
| 20 - 25 (fluctuates dependent on response status) | fast   | 600MB              |
| 15 - 20 (fluctuates dependent on response status) | normal | 400MB              |
| 10 - 15 (fluctuates dependent on response status) | slow   | 300MB              |

### Advanced Usage Guide

### Contracts

The SyncNode supports filtering your datasets to specific contracts in order to increase performance and decrease resource usage. To filter, follow the steps below

1. Create a file in the root directory `./contracts.txt`
2. Fill the `./contracts.txt` file with contracts. Ensure there is one contract per line.
3. run `yarn start` and the SyncNode will load these contracts.

Example `./contracts.txt` File

```
0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d
0x60e4d786628fea6478f785a6d7e704777c86a7c6
0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb
0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258
0xed5af388653567af2f388e6224dc7c4b3241c544
0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270
0x49cf6f5d44e70224e2e23fdcdd2c053f30ada28b
0x23581767a106ae21c074b2276d25e5c3e136a68b
```

### Scripts

The Sync Node also has several scripts that can be used to reset the backup and database:

```
yarn purge:sales // -> DELETES all records from the sales table 
yarn purge:transfers // -> DELETES all records from the transfers table
yarn purge:asks // -> DELETES all records from the asks table 
yarn purge:bids // -> DELETES all records from the bids table
yarn purge:backup // -> Flushes the current backup

```

### GraphQl

The Sync Node exposes a GraphQl path that allows for basic querying to retrieved synced data. 

Below are two partial Schemas that show the data that can be returned:

Sales Schema:

```json
    fill_source: {
      type: GraphQLString,
      resolve: (parents): string => {
        return parents.fill_source;
      },
    },
    created_at: {
      type: GraphQLString,
      resolve: (parents): string => {
        return new Date(parents.created_at).toISOString();
      },
    },
    tx_hash: {
      type: GraphQLString,
      resolve: (parents): string => {
        return '0x' + parents.tx_hash.toString('hex');
      },
    },
```

Asks Schema:

```json

    status: {
      type: GraphQLString,
      resolve: (parents): string | null => parents.status,
    },
    token_set_id: {
      type: GraphQLString,
      resolve: (parents): string | null => parents.token_set_id,
    },
    token_set_schema_hash: {
      type: GraphQLString,
      resolve: (parents): string => {
        return parents.token_set_schema_hash
          ? '0x' + parents.token_set_schema_hash.toString('hex')
          : '';
      },
    },
```

Bids Schema: 

```json

    status: {
      type: GraphQLString,
      resolve: (parents): string | null => parents.status,
    },
    token_set_id: {
      type: GraphQLString,
      resolve: (parents): string | null => parents.token_set_id,
    },
    token_set_schema_hash: {
      type: GraphQLString,
      resolve: (parents): string => {
        return parents.token_set_schema_hash
          ? '0x' + parents.token_set_schema_hash.toString('hex')
          : '';
      },
    },
```

Transfers Schema: 

```json
id: {
    type: GraphQLString,
    resolve: (parents): string => {
      return '0x' + parents.id.toString('hex');
        },
    },
  token_contract: {
    type: GraphQLString,
    resolve: (parents): string => {
      return parents.token_contract
        ? '0x' + parents.token_contract.toString('hex')
        : '';
        },
    },
```

To view the complete models, checkout the [Schema.ts](https://github.com/reservoirprotocol/reservoir-sync-node/blob/main/src/server/Schema.ts) file.

View the interaction examples below

**Sales Request:**

```
curl --location --globoff 'https://your-server.com/graphql?query={sale(offset%3A%25200){block%20fill_source%20created_at%20tx_hash}}' \
--header 'Authorization;' \

```

**Ask Request**

```
curl --location --globoff 'https://your-server.com/graphql?query={ask(offset%3A%25200){status%20token_set_id%20token_set_schema_hash}}' \
--header 'Authorization;' \
```

**Bids Request**

```
curl --location --globoff 'https://your-server.com/graphql?query={bid(offset%3A%25200){status%20token_set_id%20token_set_schema_hash}}' \
--header 'Authorization;' \
```

**Transfers Request**

```
curl --location --globoff 'https://your-server.com/graphql?query={transfer(offset%3A%25200){id%20token_contract}}' \
--header 'Authorization;' \
```

### OTA Updates

The Sync Node's express server provides a `/sync/create` endpoint, which allows you to add new contracts for backfilling and upkeep. To utilize this feature, you need to send a POST request with the required query parameters:

- `type=TABLE_NAME`
- `contract=CONTRACT_ID`

In the `type` parameter, specify either "asks", "sales",  "transfers" or "bids" based on your requirements. For the `contract` parameter, provide a valid contract ID corresponding to the blockchain your Sync Node is operating on.

An example of a complete POST request is shown below:

```curl
curl --location --request POST 'http://your-server.com/sync/create?type=ask&contract=0xed5af388653567af2f388e6224dc7c4b3241c544'
```

This request will add the specified contract to the Sync Node for backfilling and upkeeping.

### Viewer

Visiting `https://your-server.com/`will return charts two charts to visualize the status of your node. 

**In order to authorize the viewer, use the `AUTHORIZATION` ENV that was previously set**

##### Block Allocation Pie Chart

Used to display the allocation between blocks that are currently being processed VS blocks that are in queue to be processed.

##### Insertions Over Time Line Chart

Used to show a history of the amount of insertions in relation to the current time

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c16879b-Screenshot_2023-07-26_at_1.19.59_PM.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]