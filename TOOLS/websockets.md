---
title: "Websockets"
slug: "websockets"
hidden: false
createdAt: "2023-04-21T21:16:36.960Z"
updatedAt: "2023-08-03T01:23:45.514Z"
---
> 🚧 Mainnet Websockets are only available on Startup Plan
> 
> Goerli (testnet) websockets are available on our Free Plan. Mainnet chains (eg. Ethereum) require the Startup Plan or higher.
> 
> [Learn more about Reservoir subscription plans here](https://reservoir.tools/pricing).

# Overview

The Reservoir websocket service allows developers to establish a connection and obtain real-time event updates, eliminating the requirement for constant polling. You can subscribe to events, and optionally provide a filter object to narrow down events based on specific tags. 

There are two types of events, `core` events, and `derived` events. Core events are pure events on the first layer of data, such as a new sale, listing, transfer, and are useful for syncing data streams. Derived events build ontop of our first layer data by optimizing for certain use cases. For example, our `top-bid.changed` event is useful for notifying users when the top bid of a collection changes.

Please note, there is no specific limit on the number of tags (`contract`, `source`, etc.) you can subscribe to. However, subscribing to a large number of tags may affect the performance of your Node.js server and the websocket connection. It's recommended to keep the number of subscriptions within a reasonable limit to ensure smooth operation.

Refer to the table below for a list of supported events and tags.

### Core Events

| Event                | Tags                                | Event Description                                                                 |
| :------------------- | :---------------------------------- | :-------------------------------------------------------------------------------- |
| `ask.created`        | `contract`,`source`,`maker`,`taker` | Triggered on new ask creation.                                                    |
| `ask.updated`        | `contract`,`source`,`maker`,`taker` | Triggered on ask update (filled, expiry, cancellation, approval, balance change). |
| `bid.created`        | `contract`,`source`,`maker`,`taker` | Triggered on new bid creation.                                                    |
| `bid.updated`        | `contract`,`source`,`maker`,`taker` | Triggered on bid update (filled, expiry, cancellation, approval, balance change). |
| `sale.created`       | `contract`,`maker`,`taker`          | Triggered on a new sale.                                                          |
| `sale.updated`       | `contract`,`maker`,`taker`          | Triggered when we update a sale.                                                  |
| `sale.deleted`       | `contract`,`maker`,`taker`          | Triggered when a sale gets deleted (in case of chain re-organization).            |
| `transfer.created`   | `address`,`from`,`to`               | Triggered when a transfer is created.                                             |
| `transfer.updated`   | `address`,`from`,`to`               | Triggered when we update a transfer.                                              |
| `transfer.deleted`   | `address`,`from`,`to`               | Triggered when an nft transfer is deleted (re-org).                               |
| `token.created`      | `contract`                          | Triggered when a token is created (minted).                                       |
| `token.updated`      | `contract`                          | Triggered when a token is updated.                                                |
| `collection.created` | `id`                                | Triggered when a collection is created (first token minted)                       |
| `collection.updated` | `id`                                | Triggered when a collection is updated.                                           |

We also allow subscribing with `*`to subscribe to all core events. Additionally, `event.*` subscribes to all of the various events under a main event, for example `sale.*` will subscribe you to `sale.created`, `sale.updated`,`sale.deleted`. Filtering is also supported, but please note that there might be unexpected behavior from filtering on all core events via `*` due to the different events having variable tags for filtering.

### Derived Events

| Event             | Tags                | Event Description                |
| :---------------- | :------------------ | :------------------------------- |
| `top-bid.changed` | `contract`,`source` | Triggered on new top bid change. |

## Authentication

The Websocket Service utilizes the same API key for authentication as our other APIs, and it does not impact the rate limits associated with your API key tier.

| Chain           | Url                                 |
| :-------------- | :---------------------------------- |
| Mainnet         | `wss://ws.reservoir.tools`          |
| Goerli          | `wss://ws-goerli.reservoir.tools`   |
| Polygon         | `wss://ws-polygon.reservoir.tools`  |
| Arbitrum        | `wss://ws-arbitrum.reservoir.tools` |
| Optimism        | `wss://ws-optimism.reservoir.tools` |
| BNB Smart Chain | `wss://ws-bsc.reservoir.tools`      |

To connect, provide your API key as a query param in the connection url:

```
const wss = new ws(`wss://ws.reservoir.tools?api_key=${YOUR_API_KEY}`);
```

> 🚧 The websocket server needs to restart to deploy updates
> 
> The websocket server uses a rolling restart mechanism to deploy new changes. This will disconnect you and require you to reconnect to the websocket server. There is no downtime, as you are only disconnected once the new server is up and running. Please make sure to include logic in your implementation to handle these restarts, and reconnect accordingly.

## Interacting with the Websocket

Before sending any messages over the Websocket, wait for a ready message back from the server. The message looks like:

```json
{
  	// The type of operation
	"type": "connection",
   	// The status of the operation
	"status": "ready",
	"data": {
     	// Your socket id for debugging purposes
		"id": "9nqpzwmwh86"
	}
}
```

### Subscribing

Below are examples on how to subscribe to a websocket. Besides the websocket alone, you can choose filters, exclusions, and changed types.

#### Subscription (General)

```json
{
	"type": "subscribe",
	"event": "ask.created",
}
```

#### Subscription with Filters

```json
{
  "type": "subscribe",
  "event": "collection.updated",
  "filters": {
    "id": "0xd774557b647330c91bf44cfeab205095f7e6c367"
    // can optionally filter by multiple tags at once by using an array
    // "contract": [
    //   			 "0x0000c3Caa36E2d9A8CD5269C976eDe05018f0000",
    //         "0x0000c4Caa36E2d9A8CD5269C976eDe05018f0000"
    // ]
  }
}
```

#### Subscription with Exclude

You can also exclude events by certain sources when the source is a valid tag.

```json
{
  "type": "subscribe",
  "event": "bid.created",
  "exclude": {
    "source": ["opensea.io"]
  }
}
```

#### Subscription with Changed

This is to filter by what changed in `.updated` events

```json
{
  "type": "subscribe",
  "event": "token.updated",
  "changed": "collection_id"
}
```

#### Subscription Response

In you're response, your filters, changed, and exclude will be repeated back. This is an example of what might be returned.

```json
{
	"type": "subscribe",
	"status": "success",
	"data": {
		"event": "ask.created",
    	// Blank object if no filter is passed
		"filters": {
			"contract": "0x404e739c9d383efc36d3ee85fdceed53212104b2"
		}
	}
}
```

**Note:**  While there are no hard limits for number of subscriptions you can have, we recommend to manage your subscriptions efficiently and unsubscribe from channels when they are no longer needed. 

### Unsubscribing

```json
{
	"type": "unsubscribe",
	"event": "ask.created",
  	// Tags to filter events by, leave blank to not filter by any tags
 	"filters": {
   		"contract": "0x0000c3Caa36E2d9A8CD5269C976eDe05018f0000"
 	 }
}
```

#### Unsubscribe Response

```json
{
	"type": "unsubscribe",
	"status": "success",
	"data": {
		"event": "top-bid.changed"
	}
}
```

## Connecting Examples

### Javascript

```
npm install ws
```

```javascript
const ws = require('ws');

// You can get your API key from https://reservoir.tools
const YOUR_API_KEY = '';

// goerli: wss://ws.dev.reservoir.tools
const wss = new ws(`wss://ws.reservoir.tools?api_key=${YOUR_API_KEY}`);

wss.on('open', function open() {
    console.log('Connected to Reservoir');

    wss.on('message', function incoming(data) {
        console.log('Message received: ', JSON.stringify(JSON.parse(data)));

        // When the connection is ready, subscribe to the top-bids event
        if (JSON.parse(data).status === 'ready') {
            console.log('Subscribing');
            wss.send(
                JSON.stringify({
                    type: 'subscribe',
                    event: 'top-bid.changed',
                }),
            );

            // To unsubscribe, send the following message
            // wss.send(
            //     JSON.stringify({
            //         type: 'unsubscribe',
            //         event: 'top-bid.changed',
            //     }),
            // );
        }
    });
});

```

### Python

```
pip install websockets
```

```python
import asyncio
import json
import websockets

# You can get your API key from https://reservoir.tools
api_key = ''

# goerli: wss://ws.dev.reservoir.tools
wss_url = f'wss://ws.reservoir.tools?api_key={api_key}'

async def subscribe_top_bids():
    async with websockets.connect(wss_url) as websocket:
        print('Connected to Reservoir')

        async for data in websocket:
            message = json.loads(data)
            print('Message received:', message)

            if message.get('status') == 'ready':
                print('Subscribing')
                await websocket.send(
                    json.dumps({
                        'type': 'subscribe',
                        'event': 'top-bid.changed',
                    }),
                )

                # To unsubscribe, send the following message
                # await websocket.send(
                #     json.dumps({
                #         'type': 'unsubscribe',
                #         'event': 'top-bid.changed',
                #     }),
                # )

asyncio.run(subscribe_top_bids())

```

### Golang

```
go get github.com/gorilla/websocket
```

```go
package main

import (
	"encoding/json"
	"fmt"
	"log"

	"github.com/gorilla/websocket"
)

// You can get your API key from https://reservoir.tools
const apiKey = ""

func main() {
	// goerli: wss://ws.dev.reservoir.tools
	url := fmt.Sprintf("wss://ws.reservoir.tools?api_key=%s", apiKey)
	conn, _, err := websocket.DefaultDialer.Dial(url, nil)
	if err != nil {
		log.Fatal("Error connecting to Reservoir: ", err)
	}
	defer conn.Close()

	fmt.Println("Connected to Reservoir")

	var message map[string]interface{}
	for {
		_, p, err := conn.ReadMessage()
		if err != nil {
			log.Println("Error reading message: ", err)
			break
		}

		err = json.Unmarshal(p, &message)
		if err != nil {
			log.Println("Error parsing message: ", err)
			continue
		}

		fmt.Println("Message received: ", message)

		// When the connection is ready, subscribe to the top-bids event
		if message["status"] == "ready" {
			fmt.Println("Subscribing")
			err = conn.WriteJSON(map[string]interface{}{
				"type":    "subscribe",
				"event": "top-bid.changed",
			})
			if err != nil {
				log.Println("Error subscribing: ", err)
				break
			}

			// To unsubscribe, send the following message
			// err = conn.WriteJSON(map[string]interface{}{
			//     "type":    "unsubscribe",
			//     "event": "top-bid.changed",
			// })
			// if err != nil {
			//     log.Println("Error unsubscribing: ", err)
			//     break
			// }
		}
	}
}

```

### Rust

```
[dependencies]
serde_json = "1.0.73"
```

```rust
use serde_json::json;
use ws::{Builder, CloseCode, Error, Handler, Message, Result, Sender};

struct Client {
    out: Sender,
}

impl Handler for Client {
    fn on_open(&mut self, _: Handshake) -> Result<()> {
        println!("Connected to Reservoir");
        Ok(())
    }

    fn on_message(&mut self, msg: Message) -> Result<()> {
        let message: serde_json::Value = serde_json::from_str(&msg.to_string()).unwrap();
        println!("Message received: {:?}", message);

        if message["status"] == "ready" {
            println!("Subscribing");
            self.out.send(json!({
                "type": "subscribe",
                "event": "top-bid.changed",
            }))?;

            // To unsubscribe, send the following message
            // self.out.send(json!({
            //     "type": "unsubscribe",
            //     "event": "top-bid.changed",
            // }))?;
        }
        Ok(())
    }

    fn on_close(&mut self, code: CloseCode, reason: &str) {
        match code {
            CloseCode::Normal => println!("Connection closed normally"),
            CloseCode::Away => println!("Connection closed because server is going away"),
            _ => println!("Connection closed with code: {:?} for reason: {}", code, reason),
        }
    }

    fn on_error(&mut self, err: Error) {
        println!("Error: {:?}", err);
    }
}

fn main() {
    // You can get your API key from https://reservoir.tools
    let api_key = "";

    // goerli: wss://ws.dev.reservoir.tools
    let url = format!("wss://ws.reservoir.tools?api_key={}", api_key);

    Builder::new()
        .build(|out| Client { out })
        .unwrap()
        .connect(url)
        .unwrap();
}

```