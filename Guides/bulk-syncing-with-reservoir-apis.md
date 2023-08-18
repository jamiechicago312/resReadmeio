---
title: "Bulk Syncing with Reservoir APIs"
slug: "bulk-syncing-with-reservoir-apis"
excerpt: "This guide will walk you through working with various Reservoir APIs, to backfill and synchronize data effortlessly."
hidden: false
createdAt: "2023-04-19T18:27:50.022Z"
updatedAt: "2023-05-12T17:22:03.240Z"
---
Welcome to our comprehensive guide focused on optimizing your interactions with Reservoir's APIs, particularly targeting efficient data synchronization. 

In the following guides, we will explore various features and strategies to enhance your data syncing process:

- **Overview of Data Synchronization**: A high-level introduction to the concept of data synchronization and its significance in ensuring data consistency and reliability.

- **Optimizing Data Scope**: A strategy to accelerate the syncing process by focusing on the data you care about, using the `contracts` parameter.

- **Parallel Data Processing**: A deep dive into strategies like data chunking to ensure efficient and faster data synchronization, using `startTimestamp` and `endTimestamp` parameters.

- **Handling Continuations**: An exploration of how to manage and leverage the `continuation` property for effective pagination.

- **Advanced Optimizations**: A look at additional techniques like setting the right polling interval for more efficient data syncing.

We hope this guide empowers you with the knowledge to get the most out of Reservoir's APIs, making data synchronization a breeze. Happy syncing!

> 📘 #### Reservoir Sync Node
> 
> Reservoir Sync Node is our in-house TypeScript project, built to utilize the logic outlined in the following guides. It supports backfilling and Up-Keeping sales, asks, and bids data. 
> 
> We invite you to explore and see how it applies these strategies. Check it out on our GitHub repository: [Reservoir Sync Node](https://github.com/reservoirprotocol/reservoir-sync-node).