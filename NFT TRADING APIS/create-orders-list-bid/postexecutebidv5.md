---
title: "Create bids (offers)"
slug: "postexecutebidv5"
excerpt: "Generate bids and submit them to multiple marketplaces.\n\n Notes:\n\n- Please use the `/cross-posting-orders/v1` to check the status on cross posted bids.\n\n- We recommend using Reservoir SDK as it abstracts the process of iterating through steps, and returning callbacks that can be used to update your UI."
hidden: false
createdAt: "2023-03-24T14:10:57.689Z"
updatedAt: "2023-08-18T15:11:30.912Z"
---
> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

> 📘 How to check cross posted order status?
> 
> When cross posting orders to OpenSea it's important to check the status using the [cross posting orders API](https://docs.reservoir.tools/reference/getcrosspostingordersv1).