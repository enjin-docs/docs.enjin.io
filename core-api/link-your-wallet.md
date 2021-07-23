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

