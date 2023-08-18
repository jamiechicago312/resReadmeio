---
title: "Websocket best practices"
slug: "best-practices"
hidden: false
createdAt: "2023-06-23T00:04:35.035Z"
updatedAt: "2023-07-05T22:08:07.613Z"
---
This document includes some best practices to maintain a continuous stream of data over the Reservoir websocket.

# Maintaining a Connection

When developing with the Reservoir websocket it is important to note that the websocket server needs to restart to deploy updates. The websocket server uses a rolling restart mechanism to deploy new changes. This will disconnect you and require you to reconnect to the websocket server. There is no downtime, as you are only disconnected once the new server is up and running. 

To handle this properly, a proper implementation should listen to when the websocket is closed, and should re-connect once it detects a close event. Here is an example socket class in javascript of how this can look like:

```typescript
import * as ws from 'ws';

export class WebsocketClient {
    private ws: ws;

    public connect = () => {
        this.ws = new ws(`wss://ws.reservoir.tools?api-key=${YOUR_API_KEY}`);

        this.ws.on('open', () => {
            console.log('connected');
            this.subscribe();
        });

        this.ws.on('message', data => {
            this.handleMessage(data);
        });

        this.ws.on('close', () => {
            console.log('closed');
            this.connect();
        });
    };

    public handleMessage = async (data: any) => {
        const message = JSON.parse(data);
        // add your logic here
    };

    public subscribe = () => {
        this.ws.send(
            JSON.stringify({
                type: 'subscribe',
                event: '*',
            }),
        );
    };
}

```

Make sure that your websocket library supports listening to close events and re-connecting when they occur. 

## Heartbeats

Heartbeats are **not** necessary to be manually sent to maintain your connection to the Reservoir websocket. The majority of modern websocket clients have heartbeats built into the connection and are automatically managed. 

[Most websocket libraries after 2011 support this.](https://datatracker.ietf.org/doc/html/rfc6455#section-5.5.2)

## Subscriptions

Subscriptions are not maintained between your connections, and if your connection drops, you will need to re-subscribe to all the events you were subscribed to. Try to persist your subscriptions somewhere else in your implemnetation, and refer to it for re-creating subscriptions when a connection drops.