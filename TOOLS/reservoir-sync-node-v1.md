---
title: "Reservoir Sync Node V1"
slug: "reservoir-sync-node-v1"
excerpt: "A customizable lightweight indexer based on the Reservoir indexer. Continuously sync sales, asks, and bids into your infrastructure."
hidden: true
metadata: 
createdAt: "2023-05-09T21:17:11.557Z"
updatedAt: "2023-07-28T19:34:30.907Z"
---
## Introduction

The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node) provides an easy-to-launch syncing system to keep up to date and retrieve bulk NFT data from the Reservoir Data Lake. Currently, our sync node supports backfilling & live syncing for  [bids](https://docs.reservoir.tools/docs/syncing-bids), [asks](https://docs.reservoir.tools/docs/syncing-asks) and [sales ](https://docs.reservoir.tools/docs/syncing-sales)data.  We highly recommend utilizing the sync node when it comes to handling the task of backfilling historical data. Current backfill time is about 20-40 mins for about 2-3 million rows of data. This methodology provides a streamlined way to manage large datasets effectively, while also reducing time & API usage.

### Installation

To install the required dependencies for the Light Sync Node, run:

```bash
yarn installl
```

### Configuration - ENV

Included is an example .env file (example.env). Rename it to .env and configure as shown below:

```
# Database configuration
DATABASE_URL=your-postgres-database-url # (Required) PostgresSQL database to pipe data into

# Server configuration

PORT= # (Required) Port to spawn the server on
AUTHORIZATION= # (Required) Server authorization string

# Logger configuration
# (Optional) Datadog app name to send internal logs to
#DATADOG_APP_NAME=
# (Optional) Datadog api key for the above app
#DATADOG_API_KEY=
# Databse Configuration
DATABASE_URL=your-postgres-database-url # (Required) Database to pipe data into

# Backup configuration
# (Optional) Sign up for a free redis cloud instance http://redis.com/try-free/
# REDIS_URL= 

# Syncer configuration
# (Required) Enable or disable the syncing of sales (1 = true | 0 = false)
SYNC_SALES=0 
# (Required) Enable or disable the syncing of asks (1 = true | 0 = false)
SYNC_ASKS=0
# (Required) Enable or disable the syncing of bids (1 = true | 0 = false)
SYNC_BIDS=0

CHAIN=mainnet # (Required) Chain to sync
API_KEY=your_reservoir_api_key # (Required) Reservoir API key - Sign up for free https://reservoir.tools/

# (Optional) (Max 5)  Contracts to filter by - i.e., Only these contracts will be indexed. 
# CONTRACTS=contract1,contract2,contract3

# (Optional) (Default: 1) Number of workers to be used by the managers to parallelize days in months
# WORKER_COUNT=

# (Optional) (Default: 1) Number of managers to be used by the syncers, increase this to increase the amount of months indexed at a time
# MANAGER_COUNT=
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
> 2. It triggers the script `npx prisma migrate resolve --applied 20230628214741_sync_node_migration` to form a baseline of migration history in your database. This baseline is required since Prisma needs to confirm that your database schema is in sync with your schema model. For a comprehensive understanding, please refer to the Prisma documentation on [baselining](https://www.prisma.io/docs/guides/migrate/developing-with-prisma-migrate/baselining).
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

### Advanced Usage Guide

#### Scripts

The Sync Node also has several scripts that can be used to reset the backup and database:

```
yarn purge:sales // -> DELETES all records from the sales table 
yarn purge:asks // -> DELETES all records from the asks table 
yarn purge:bids // -> DELETES all records from the bids table
yarn purge:backup // -> Flushes the current backup

```

#### GraphQl

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

#### OTA Updates

The Sync Node's express server provides a `/sync/create` endpoint, which allows you to add new contracts for backfilling and upkeep. To utilize this feature, you need to send a POST request with the required query parameters:

- `type=TABLE_NAME`
- `contract=CONTRACT_ID`

In the `type` parameter, specify either "asks", "sales", or "bids" based on your requirements. For the `contract` parameter, provide a valid contract ID corresponding to the blockchain your Sync Node is operating on.

An example of a complete POST request is shown below:

```curl
curl --location --request POST 'http://your-server.com/sync/create?type=ask&contract=0xed5af388653567af2f388e6224dc7c4b3241c544'
```

This request will add the specified contract to the Sync Node for backfilling and upkeeping.