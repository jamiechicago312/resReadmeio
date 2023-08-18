---
title: "Syncing Sales"
slug: "syncing-sales"
hidden: false
createdAt: "2023-04-27T18:08:33.949Z"
updatedAt: "2023-08-16T13:26:42.825Z"
---
> 🚧 We Recommend Reservoir Sync Node
> 
> Looking to bulk sync sales data into your database? We recommend using the Reservoir Sync Node. It's an In-house TypeScript project built to leverage the logic described below into a system powered by our API. It provides support for backfilling and updating sales, bids, and asks data.
> 
> Want to get started?  Check out the [documentation]('https://docs.reservoir.tools/reference/reservoir-sync-node').  
> Just looking for inspiration? Visit the [repository](https://github.com/reservoirprotocol/reservoir-sync-node)

### Backfilling - Introduction

Backfilling refers to the retrieval of historical sales data. This recursive process begins with an initial request sent to the Reservoir Sales API. With each response, you will receive a "continuation" token, which you append to your next request. This enables you to paginate through the results, moving forward in time with each request until you reach the sales data for the present day.

To kick off this process, you need to send an initial request. An example of this request is shown below:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/sales/v6?includeDeleted=true&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

| Parameter           | Description                                               |
| :------------------ | :-------------------------------------------------------- |
| includeDeleted=true | This parameter ensures deleted sales are returned         |
| sortBy=updatedAt    | This parameter orders the results by their updatedAt date |
| sortDirection=asc   | This parameter sorts the results in an ascending manner   |
| limit=1000          | This parameter increases the count of results to return   |

When you receive a response, it should resemble the following structure:

```json
{
  "sales": [], //... array of sales data 
  "continuation": "" // Continuation token to paginate,
}
```

The continuation property in the response is key to this process. You append this value to your next query and send the request again. This returns the next set of sales data. Continue this procedure of appending the continuation token and sending requests until a response comes back without a continuation token. The absence of a continuation token indicates that you've fetched all the available data up to the present moment, completing the backfilling process.

### Backfilling - Advanced Optimizations

#### Optimizing Data Scope

One effective strategy to expedite the backfilling process is to narrow down the data you fetch to only include the sales data from the contracts you are interested in. The **contracts** parameter can be used to limit the scope of your data and subsequently reduce the total number of requests made. This ensures that only the sales data related to the specified contracts are returned.

The contract parameter can be used as follows: `contract=contractOne&contract=contractTwo`

Here's an example of a request with the contract parameter:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/sales/v6contract=contractOne&contract=contractTwo&includeDeleted=contrue&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

#### Parallel Data Processing

Reservoir's sales table contains an extensive number of records, exceeding 76 million. Sequentially paginating through each request would entail a prolonged duration. To mitigate this, the [Sales API](https://docs.reservoir.tools/reference/getsalesv5) introduces two supplementary query parameters: **startTimestamp**, **endTimestamp**.

 The **startTimestamp** and **endTimestamp** parameters are designed to partition the data into smaller segments that can be processed concurrently by your system design. The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node), a TypeScript project, showcases the utilization of these parameters. It employs **startTimestamp** and **endTimestamp** to segregate data into monthly and daily intervals.

Prior to incorporating these parameters, you must layout how you will segment the data. For the sake of this guide, we'll partition the data into monthly sets (The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node) illustrates data segmentation into both monthly and daily intervals).

Get started by executing an initial request without the **startTimestamp** and **endTimestamp** as shown below:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/sales/v6?includeDeleted=true&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

From the returned sales array, your first task is to parse and store the **updatedAt** property of the final sale in the array. This **updatedAt** property is an ISO date which will be transformed into a UNIX timestamp. This timestamp then serves as the reference point/start point of when the data should be returned from.

```json
{
  "sales": [
    {
      "updatedAt":"2023-04-27T17:46:50.659Z" // ISO date
		}
  ], 
  "continuation": "",
}
```

After parsing the date and converting it to a UNIX timestamp, we have our **startTimestamp**. The next step involves incrementing this timestamp by a month to create our **endTimestamp**.

```
(ISO) 2023-04-27T17:46:50.659Z |Conversion| (UNIX) 1682617610 |Increment| (UNIX) 1685246354
```

Upon incrementing the timestamp, we now have both our **startTimestamp** and **endTimestamp** parameters, which define our first chunk of data. Next, append these parameters to your request and proceed to execute it:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/sales/v6?startTimestamp=1682617610&endTimestamp=1685246354&includeDeleted=true&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

Upon receiving a response, you will receive sales data from that period of time as defined by **startTimestamp** & **endTimestamp**. The "continuation" property will return either a string or null. A null value signifies that all the data for the provided **startTimestamp** and **endTimestamp** chunk has been retrieved. Conversely, a string value indicates there is additional data within that specific time chunk that needs to be paginated through using the continuation property.

The process of partitioning the data into monthly chunks may yield a parameter table similar to the one below:

| startTimestamp           | endTimestamp             |
| :----------------------- | :----------------------- |
| 1682617610 (Jan. 2018)   | 1685246354 (Feb. 2018)   |
| 1685246354 (Feb. 2018    | 1685246354 (March. 2018) |
| 1685246354 (March. 2018) | 1685246354 (Apr. 2018)   |

The same method can be adapted to smaller data chunks by adjusting the increment value for the **startTimestamp**. For instance, if you intend to segment the data by days, your **startTimestamp** should be incremented day by day, rather than month by month.

| startTimestamp        | endTimestamp          |
| :-------------------- | :-------------------- |
| 1682617610 (Jan. 1st) | 1682617610 (Jan. 2nd) |
| 1682617610 (Jan. 2nd) | 1682617610 (Jan. 3rd) |
| 1682617610 (Jan. 4th) | 1682617610 (Jan. 5th) |

By adopting this chunking strategy, you can process distinct data segments concurrently, significantly reducing the total time needed to backfill all historical sales data.

### Up-Keeping - Introduction

Once you have reached the present date you can now begin the process of Up-Keeping. Up-Keeping is the process of polling the API in order to stay up to date with the latest sales. Much of the logic in backfilling is shared in Up-Keeping.

To get started you need to fire of a request using the **startTimestamp** parameter. The parameter should be set to the current/present time. Sending the request with this parameter will ensure that you only return results that are just happening. 

The request is shown below:

```
curl --request GET \
     --url 'https://api.reservoir.tools/sales/v6?startTimestamp=1682617610&includeDeleted=true&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

```
{
  "sales": [
    {
      "id":"" // Unique sale identifier
		}
  ], 
  "continuation": null,
}
```

Once you have received a response, ensure to store the returned results and take note of the 'id' properties of the returned sales. These will be utilized to filter out duplicate results. When firing this request, there are two possible scenarios you might encounter:

1. **Continuation property is null**
   - If the **continuation** property is null, you should wait a few seconds and resend the request. There's a chance that on resending the request, you might receive duplicate results, as the response uses pagination only when there are more than 1000 results. In such a situation, use the previously stored 'id' set from the array of received sales to filter out unprocessed sales. This scenario typically arises when you receive less than 1000 sales.

2. **Continuation property is not null**
   - If the **continuation** property is not null, you should use the continuation to paginate through the results. The continuation string is returned only when there are more than 1000 results. If there are fewer results, you will not receive a continuation. Resend the request with the newly received continuation and repeat the process described above.

### Up-Keeping - Advanced Optimizations

#### Polling Interval

We recommend setting a polling interval of one request per minute. This approach ensures that you allocate adequate time for approximately 1000 sales to process, reducing the necessity of filtering out duplicates. Depending on your specific use case, you can adjust this interval to be shorter or longer.