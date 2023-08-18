---
title: "How to Protect Your API Key"
slug: "how-to-protect-your-api-key"
excerpt: "Best practices for protecting your API key and how to secure it from unauthorized access"
hidden: false
createdAt: "2023-04-27T19:15:59.476Z"
updatedAt: "2023-06-16T21:01:53.033Z"
---
Protecting your API key is an important step to help ensure the security of your account. Here are some best practices to secure your API key from unauthorized access:

1. Utilize a proxy server when building a consumer-facing application. All API calls should be routed through the proxy, where the endpoint and query parameters can be parsed to generate the desired API call. An example of a proxy server and its parsing logic can be found in [Reservoir Market v2](https://github.com/reservoirprotocol/marketplace-v2/blob/main/pages/api/reservoir/%5B...slug%5D.ts) which employs a catch all API route using Next.js.
2. Implement the correct CORS rules to ensure other applications can't use your proxy to piggy-back your API key.
3. Consider using IP filtering/whitelisting to block requests that don't implement CORS (such as curl, postman, etc.).
4. Configure additional API key security options on the Apps page of your [Reservoir dashboard](https://dashboard.reservoir.tools/).

![](https://files.readme.io/aba97a3-Screen_Shot_2023-06-16_at_4.57.55_PM.png)

By following these best practices, you can help protect your API key from malicious activities and any additional costs associated with unauthorized access.