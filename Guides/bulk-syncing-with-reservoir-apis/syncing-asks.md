---
title: "Syncing Asks"
slug: "syncing-asks"
hidden: false
createdAt: "2023-05-04T18:12:39.631Z"
updatedAt: "2023-08-16T13:18:18.288Z"
---
> 🚧 We Recommend Reservoir Sync Node
> 
> Looking to bulk sync asks data into your database? We recommend using the Reservoir Sync Node. It's an In-house TypeScript project built to leverage the logic described below into a system powered by our API. It provides support for backfilling and updating sales, bids, and asks data.
> 
> Want to get started?  Check out the [documentation]('https://docs.reservoir.tools/reference/reservoir-sync-node').  
> Just looking for inspiration? Visit the [repository](https://github.com/reservoirprotocol/reservoir-sync-node).

### Backfilling - Introduction

Backfilling refers to the retrieval of historical asks data. This recursive process begins with an initial request sent to the asks API. With each response, you will receive a "continuation" token, which you append to your next request. This enables you to paginate through the results, moving forward in time with each request until you reach the asks data for the present day.

To get started an the checkout the example request below:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/orders/asks/v5?includeDeleted=true&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

| Parameter         | Description                                                                            |
| :---------------- | :------------------------------------------------------------------------------------- |
| sortBy=updatedAt  | This parameter orders the results by their updatedAt date                              |
| sortDirection=asc | This parameter sorts the results in an ascending manner                                |
| limit=1000        | This parameter increases the count of results to return                                |
| status=active     | This parameter ensures that only active orders are returned. E.g Not Expired/Cancelled |

When you receive a response, it should resemble the following structure:

```json
{
  "orders": [], //... array of orders data 
  "continuation": "" // Continuation token to paginate,
}
```

The continuation property in the response is key to this process. You append this value to your next query and send the request again. This returns the next set of asks/bids data. Continue this procedure of appending the continuation token and sending requests until a response comes back without a continuation token. The absence of a continuation token indicates that you've fetched all the available data up to the present moment, completing the backfilling process.

### Backfilling - Advanced Optimizations

#### Optimizing Data Storage

Storing all of the asks can lead to substantial data volume, potentially resulting in high database costs. To alleviate this issue, you can implement client-side filtering using contracts to exclude irrelevant data. This can be achieved by using the contract ID parameter of the returned ask and then selectively storing the data based on whether you care for that particular contract or not.

#### Parallel Data Processing

Reservoir's asks table contains an extensive number of records. Sequentially paginating through each request would entail a prolonged duration. To mitigate this, the [Asks](https://docs.reservoir.tools/reference/getordersasksv4) API introduces two supplementary query parameters: **startTimestamp**, **endTimestamp**.

 The **startTimestamp** and **endTimestamp** parameters are designed to partition the data into smaller segments that can be processed concurrently by your system design. The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node), a TypeScript project, showcases the utilization of these parameters. It employs **startTimestamp** and **endTimestamp** to segregate data into monthly and daily intervals.

Prior to incorporating these parameters, you must layout how you will segment the data. For the sake of this guide, we'll partition the data into monthly sets (The [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node) illustrates data segmentation into both monthly and daily intervals). We'll be sending this request to the **Asks** API, however the logic is exactly the same for **Orders**.

Get started by executing an initial request without the **startTimestamp** and **endTimestamp** as shown below:

```curl
curl --request GET \
     --url 'https://api.reservoir.tools/orders/asks/v5?status=active&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

From the returned asks array, your first task is to parse and store the **updatedAt** property of the final ask in the array. This **updatedAt** property is an ISO date which will be transformed into a UNIX timestamp. This timestamp then serves as the reference point/start point of when the data should be returned from.

```json
{
  "orders": [
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
     --url 'https://api.reservoir.tools/orders/asks/v5?startTimestamp=1682617610&endTimestamp=1685246354&status=active&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

Upon receiving a response, you will receive asks data from that period of time as defined by **startTimestamp** & **endTimestamp**. The "continuation" property will return either a string or null. A null value signifies that all the data for the provided **startTimestamp** and **endTimestamp** chunk has been retrieved. Conversely, a string value indicates there is additional data within that specific time chunk that needs to be paginated through using the continuation property.

The process of partitioning the data into monthly chunks may yield a parameter table similar to the one below:

| startTimestamp           | endTimestamp             |
| :----------------------- | :----------------------- |
| 1514764800 (Jan. 2018)   | 1517443200 (Feb. 2018)   |
| 1517443200 (Feb. 2018    | 1519862400 (March. 2018) |
| 1519862400 (March. 2018) | 1685246354 (Apr. 2018)   |

The same method can be adapted to smaller data chunks by adjusting the increment value for the **startTimestamp**. For instance, if you intend to segment the data by days, your **startTimestamp** should be incremented day by day, rather than month by month.

| startTimestamp        | endTimestamp          |
| :-------------------- | :-------------------- |
| 1682617610 (Jan. 1st) | 1514851200 (Jan. 2nd) |
| 1514851200 (Jan. 2nd) | 1514937600 (Jan. 3rd) |
| 1515024000 (Jan. 4th) | 1515110400 (Jan. 5th) |

By adopting this chunking strategy, you can process distinct data segments concurrently, significantly reducing the total time needed to backfill all historical asks data.

### Up-Keeping - Introduction

Once you have reached the present date, you can start the Up-Keeping process. Up-Keeping involves polling the API to stay current with the latest asks. Much of the logic used in backfilling also applies to Up-Keeping.

To begin, send a request using the startTimestamp parameter. Set this parameter to the current or present time. By including this parameter in your request, you'll ensure that only the most recent results are returned.

The request is shown below:

```
curl --request GET \
     --url 'https://api.reservoir.tools/orders/asks/v5?startTimestamp=1682617610&status=active&sortBy=updatedAt&sortDirection=asc&limit=1000' \
     --header 'accept: */*' \
     --header 'x-api-key: demo-api-key'
```

```
{
  "orders": [
    {
      "id":"" // Unique ask identifier
		}
  ], 
  "continuation": null,
}
```

After receiving a response, make sure to store the returned results and note the 'id' properties of the retrieved asks. These 'id' properties will be used to filter out duplicate results. When sending this request, you may come across two possible scenarios:

1. **Continuation property is null**
   - If the continuation property is null, you should wait for a few seconds before resending the request. When resending, you might encounter duplicate results, since pagination is accounted for when there are only over 1000 results. In this case, utilize the previously stored 'id' set from the array of received asks to filter out unprocessed asks. This situation commonly occurs when you receive fewer than 1000 asks.

2. **Continuation property is not null**
   - If the **continuation** property is not null, you should utilize the continuation to paginate through the results. The continuation string is provided only when there are over 1000 results. If the results are fewer, you won't receive a continuation. Resubmit the request with the recently obtained continuation and follow the process outlined above.

### Up-Keeping - Advanced Optimizations

#### Dataset Filter

During the backfilling process, it's crucial to concentrate on active orders to prevent gathering obsolete or unrelated data. To accomplish this, incorporate the status=active parameter in your query. When you enter the upkeep phase, remove this parameter, allowing updates for orders that may have been canceled, expired, or experienced price changes.

#### WebSocket Optimizations

Reservoir provides real-time WebSocket events for Asks, improving efficiency by minimizing the number of requests required once you're up-to-date with the current data. To view a reference implementation of these WebSockets, check out the [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node). In this project, we increase the polling interval for our UpKeeper and mainly depend on the WebSocket to obtain real-time information.

#### Polling Interval

WWe suggest setting a polling interval of one request per minute. This strategy allows sufficient time for processing around 1000 asks, minimizing the need to filter out duplicates. Based on your unique use case, you may adjust this interval to be shorter or longer as needed.