---
description: Learn more about sending and receiving your assets
---

# Sending & Receiving

You may want to send assets to your players, request for them to send you assets, or even request for them to send each other assets.

This can all be achieved by using one simple query.

The Enjin API provides a query that allows you to send unlimited Fungible (FT) and up to 100 Non-Fungible assets (NFT) to up to 150 users, with one single transaction.&#x20;

### Step 1: Advanced Send

You can use Enjin’s advanced send query to send assets from you to your players; from your players to you, or from your players to each other.

```graphql
mutation {
  AdvancedSendAsset(
    transfers: {
      from: "WalletAddress"
      to: "WalletAddress"
      assetId: "788000000000089f"
      assetIndex: "0000000000000001"
      value: "1"
    }
  ) {
    transactionId
    id
    state
    value
    asset{name id}
    user{name}
  }
}
```

### Step 2: View Transaction Status

If you want to check the status of the advanced send transaction to find out when it has been executed, you can do so by using the following query:

```graphql
query {
  GetTransaction(id: xxxxx) {
    id
    transactionId
    title
    contract
    type
    user{id, name}
    userId
    value
    state
    accepted
    projectWallet
    project{id, name}
    asset{id, name}
  }
}
```

**Automatically Signing Transactions**

Many of these steps involve creating blockchain transactions that need to be signed via your Enjin Wallet.** **We have created a Wallet Daemon that can sign these transactions automatically.

[Here are the instructions on how to use it.](../../wallet-daemon/get-started/daemon-installation.md)

{% hint style="danger" %}
**IMPORTANT:** Please be aware that using a wallet daemon will mean that ANY transaction that is generated via your App Secret will be signed automatically. Please ensure there is no way for any unauthorized party to access your App Secret and process unapproved transactions.
{% endhint %}
