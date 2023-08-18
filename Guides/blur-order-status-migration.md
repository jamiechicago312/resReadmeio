---
title: "Blur order status migration"
slug: "blur-order-status-migration"
hidden: false
createdAt: "2023-06-10T13:20:17.600Z"
updatedAt: "2023-06-10T13:20:17.600Z"
---
Recently, we made a change to improve the robustness of our Blur listing aggregation, to ensure we have coverage of 100% of listings, including Blend listings. For most customers, no changes are required. However, for teams that are utilizing the rawData and tracking order status on-chain, you may need to update how your system works. For now, we are supporting both the old and new systems in parallel, but will soon retire the old system.

In the old system, we provided full Blur order objects, which included the order hash and expiry time. The problem with this method is that it was prone to errors and delays, and did not cover 100% of orders. In the new system, we have 100% coverage of all listings, but we don’t have full order details (hash, expiry, etc). The main difference is that instead of being able to track when orders become invalid yourself (based on expiry or on-chain events), you must rely on our events to know when the status changes (ask.updated websocket or poll the Asks API sorted by updatedAt). 

While we agree there are downsides to the new system, we believe that the benefits of 100% coverage and improved robustness are worth it. We recommend all teams migrate ASAP. If you have any questions, feel free to reach out. Remember, only teams that use the rawData are impacted. If you rely on Reservoir to keep track of the status of all orders, no changes are required.

**Old Raw Data**

```json
{  
        "fees":[  
            {  
                "rate":50,  
                "recipient":"0xaf968d74e79fd2ad24e366bff96e91f769e0aaea"  
            }  
        ],  
        "side":1,  
        "amount":"1",  
        "salt":"86794259941631656176393694721086747534",  
        "tokenId":"73644797187710155126889262417898073625983376536319089985511350696994644685538",  
        "kind":"erc721-single-token",  
        "listingTime":1686130678,  
        "trader":"0x4738c8b9e0d7b48db4056bf017d2f90b2319630d",  
        "extraParams":"0x01",  
        "collection":"0xc2e9678a71e50e5aed036e00e9c5caeb1ac5987d",  
        "nonce":"0",  
        "extraSignature":"0x000000000000000000000000000000000000000000000000000000000000001c3e6034d8a2f96370056eae3884240fbde71fae16577a9cda59a913e4de98423e21a43a3f0dd1a9f309d093b65eb89afa13474cd96918579eeea7be3024395365",  
        "signatureVersion":0,  
        "matchingPolicy":"0x0000000000dab4a563819e8fd93dba3b25bc3495",  
        "paymentToken":"0x0000000000000000000000000000000000000000",  
        "r":"0x7b7d50cd3fa4b5d143401f8732d1b663b49f1c47fb833b242efc45497a0c54c1",  
        "s":"0x638020d9e15dce49824a1ef4b9fd10bee45e3750fbc1ee8001a70b8efdc671e5",  
        "v":27,  
        "price":"376900000000000000",  
        "expirationTime":1686217078  
    }
```



**New Raw Data**

```json
{  
                "price": "0.78",  
                "tokenId": "2625",  
                "createdAt": "2023-05-30T06:18:36.000Z",  
                "collection": "0xecafeba408dd65fdc94030ec5aa99f3bd15c842c"  
            }
```