---
title: "Token Attribute"
slug: "token-attribute"
hidden: false
createdAt: "2023-07-28T00:11:42.493Z"
updatedAt: "2023-07-28T18:47:04.583Z"
---
Subscribe to `token-attribute` events to get real-time access to token attribute updates or keep a copy of Reservoir's aggregated orderbook in sync.

## How to Subscribe

View instructions [here](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket).

## Subscription Options

|             | Value                   | Description                                                                       |
| :---------- | :---------------------- | :-------------------------------------------------------------------------------- |
| **Event**   | token-attribute.created | When a token attribute is created.                                                |
|             | token-attribute.deleted | When a token attribute is deleted.                                                |
|             | token-attribute.\*      | All token attribute events (created and updated)                                  |
| **Filters** | contract                | Filter to one or more contracts (e.g. 0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) |

## Example `token-attribute.created` Payload

```json
{
    "event": "token-attribute.created",
    "tags": {
        "token_id": "5875",
        "contract": "0x932261f9fc8da46c4a22e31b45c4de60623848bf"
    },
    "changed": [],
    "data": {
        "token": {
            "contract": "0x932261f9fc8da46c4a22e31b45c4de60623848bf",
            "tokenId": "5875"
        },
        "collection": {
            "id": "0x932261f9fc8da46c4a22e31b45c4de60623848bf"
        },
        "key": "Age",
        "value": "61 week",
        "createdAt": "2023-07-28T18:43:02.872938Z",
        "updatedAt": "2023-07-28T18:43:02.872938Z"
    },
    "published_at": 1690569783064,
    "type": "event",
    "status": "success"
}
```

## Example `token-attribute.deleted` Payload

```json
{
    "event": "token-attribute.deleted",
    "tags": {
        "token_id": "5875",
        "contract": "0x932261f9fc8da46c4a22e31b45c4de60623848bf"
    },
    "changed": [],
    "data": {
        "token": {
            "contract": "0x932261f9fc8da46c4a22e31b45c4de60623848bf",
            "tokenId": "5875"
        },
        "collection": {
            "id": "0x932261f9fc8da46c4a22e31b45c4de60623848bf"
        },
        "key": "Age",
        "value": "60 weeks",
        "createdAt": "2023-07-20T20:34:36.289168Z",
        "updatedAt": "2023-07-20T20:34:36.289168Z"
    },
    "published_at": 1690569783144,
    "type": "event",
    "status": "success"
}
```