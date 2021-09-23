---
description: How to connect to the Enjin API
---

# Connect to Enjin API

Allow your app to communicate fluidly with the Enjin smart contract.

This will allow you to programmatically view wallet inventory, mint assets from your wallet, send assets from your wallet, and request assets from users' wallets.

### **Step 1: Find your App ID & AppSecret**

Firstly, you will need to locate your **AppID** and **AppSecret** on the Enjin platform.

1. Go to cloud.enjin.io \(if using Mainnet\), or jumpnet.cloud.enjin.io \(if using JumpNet\).
2. Create or select your **Project.**
   1. More information [here](https://enjin.io/help/creating-your-first-project), on how to create your project.
3. Select **Settings** in the sidebar.

You will find your **AppID** and **AppSecret** in the **Settings** panel.

### **Step 2: Generate your Authorization Token**

Go to GraphQL Playground: [https://jumpnet.cloud.enjin.io/graphql/playground](https://jumpnet.cloud.enjin.io/graphql/playground)

Generate your unique authorization token by using the following query:

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query GetPlayerAccessToken {
  AuthPlayer(id: "userName"){
    accessToken
    expiresIn
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
**IMPORTANT:** Only store your App Secret server side. Do not store your App Secret inside your executable file or hackers will be able to decompile your game and mint tokens on your behalf.
{% endhint %}

### **Step 3: Use your App Secret**

You can now use your AppSecret to run queries from your server by querying the Enjin API. You can do this either via GraphiQL PlayGround on Mainnet or on JumpNet. 

1. **Mainnet:** cloud.enjin.io/graphql/playground
2. **JumpNet:** jumpnet.cloud.enjin.io/graphqlplayground

