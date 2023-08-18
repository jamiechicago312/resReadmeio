---
title: "How is the salt generated for created listings?"
slug: "how-is-the-salt-generated-for-created-listings"
hidden: true
createdAt: "2023-04-17T14:55:55.172Z"
updatedAt: "2023-05-02T20:14:10.625Z"
---
When creating a listing, the salt is an optional parameter used to make the order unique. It is a random string that ensures that even if two orders have the same parameters, they will still be considered distinct due to the different salt values.

In most cases, you don't need to worry about generating the salt yourself, as the Reservoir SDK or the Reservoir marketplace you're using will handle it for you. However, if you want to generate a custom salt for your listing, you can do so using any random string generation method.

For example, in JavaScript, you can generate a random salt as follows:

```javascript
function generateRandomSalt() {  
  return Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);  
}

const salt = generateRandomSalt();
```

When creating a listing using the Reservoir SDK, you can pass the generated salt as a parameter in the listing creation function. Keep in mind that the salt is only necessary if you want to create.