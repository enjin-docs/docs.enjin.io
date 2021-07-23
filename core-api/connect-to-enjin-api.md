---
description: How to connect to Enjin API
---

# Connect to Enjin API

Allow your app to communicate fluidly with the Enjin smart contract.

This will allow you to programmatically view wallet inventory, mint tokens from your wallet, send tokens from your wallet, and request tokens from user wallets.

### **Step 1**

Find your **AppID** and **AppSecret** on the Enjin Platform.

1. Go to [http://jumpnet.cloud.enjin.io](http://jumpnet.cloud.enjin.io/)
2. Create or select your **Project**
3. Select **Settings** in the sidebar

You will find your **AppID** and **AppSecret** in the **Settings** panel

### **Step 2**

Go to GraphQL Playground: [https://jumpnet.cloud.enjin.io/graphql/playground](https://jumpnet.cloud.enjin.io/graphql/playground)

### **Step 3**

Generate your authorization token by using this query:

```graphql
query RetrieveAppAccessToken {
 AuthApp(id: <App ID>, secret: "<App Secret>") {
 accessToken
 expiresIn
 }
}
```

**IMPORTANT:** Only store your App Secret server side. Do not store your App Secret inside your executable file or hackers will be able to decompile your game and mint tokens on your behalf.

### **Step 4**

You can now use your AppSecret to run queries from your server by querying the Enjin API: [https://jumpnet.cloud.enjin.io/graphql](https://jumpnet.cloud.enjin.io/graphql)

