---
title: "Approvals"
slug: "approval"
hidden: true
createdAt: "2023-05-31T19:09:09.185Z"
updatedAt: "2023-07-03T22:11:08.808Z"
---
Subscribe to `approval` events to get real-time access to new/updated approvals or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|            | Value            | Description                                                            |
| :--------- | :--------------- | :--------------------------------------------------------------------- |
| **Event**  | approval.created | When a new ask is created                                              |
|            | approval.updated | When an an approval is updated.                                        |
|            | approval.\*      | All approval events (created and updated)                              |
| **Filter** | address          | A contract address (e.g. `0xb6bfb007a7cb4e07b5ef07692cc0ad0731d368a2`) |
|            | owner            | A wallet address (e.g. `0xd0d9fa1cefafb7c36ac7065a6c783e9d70f54884`)   |
|            | approval         | Boolean (`true` or `false`)                                            |

## Example `approval.created` Payload

```json
{
    "event": "approval.created",
    "tags": {
        "address": "0xb6bfb007a7cb4e07b5ef07692cc0ad0731d368a2",
        "owner": "0xd0d9fa1cefafb7c36ac7065a6c783e9d70f54884",
        "approved": true
    },
    "data": {
        "address": "0xb6bfb007a7cb4e07b5ef07692cc0ad0731d368a2",
        "block": 17331823,
        "timestamp": 1684965047,
        "owner": "0xd0d9fa1cefafb7c36ac7065a6c783e9d70f54884",
        "operator": "0x1e0049783f008a0085193e00003d00cd54003c71",
        "approved": true,
        "txHash": "0xcc394c65802cadc6fd6ccd510e5967cbb07ac595a1464995b3584f58ab6bf471",
        "logIndex": 221,
        "batchIndex": 1
    },
    "published_at": 1684965051851,
    "type": "event",
    "status": "success"
}
```

## Example `approval.updated` Payload

```json
{
    "event": "approval.updated",
    "tags": {
        "address": "0xb6bfb007a7cb4e07b5ef07692cc0ad0731d368a2",
        "owner": "0xd0d9fa1cefafb7c36ac7065a6c783e9d70f54884",
        "approved": true
    },
    "data": {
        "address": "0xb6bfb007a7cb4e07b5ef07692cc0ad0731d368a2",
        "block": 17331823,
        "timestamp": 1684965047,
        "owner": "0xd0d9fa1cefafb7c36ac7065a6c783e9d70f54884",
        "operator": "0x1e0049783f008a0085193e00003d00cd54003c71",
        "approved": true,
        "txHash": "0xcc394c65802cadc6fd6ccd510e5967cbb07ac595a1464995b3584f58ab6bf471",
        "logIndex": 221,
        "batchIndex": 1
    },
    "published_at": 1684965051851,
    "type": "event",
    "status": "success"
}
```