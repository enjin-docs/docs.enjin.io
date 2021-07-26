---
description: Learn how to link your Wallet
---

# Link Your Wallet

Verify your wallet address so it can approve blockchain transactions sent from your app.

### **Step 1**

To run processes that need to be approved by your developer wallet, you will need to link your wallet to your **Developer ID**. You can do this by running the following query through [GraphQL Playground](http://jumpnet.cloud.enjin.io/).

```graphql
query GetIdentities($page: Int) {
  EnjinIdentities(pagination: {page: $page, limit: 50}) {
    id
    linkingCode
    linkingCodeQr
    wallet {
      ethAddress
    }
  }
}
```

Using this query, should return various pieces of information that will help you with further integration, such as:

* The App Id.
* The Linking Code.
* The Linking Code QR \(This is rather useful, you can copy the URL of the linking code QR in a new tab, and scan with the Enjin Wallet to link your Identity ID\).
* The wallet address is associated with the identity ID.

### **Step 2**

Once you have your **Linking Code**, navigate to the **Linked Apps** section in your **Enjin Wallet**.

The wallet will ask you for your Linking Code.

Once you have linked your wallet to your **Developer ID**, ****you will be able to approve transaction requests that are programmatically sent from your app.

