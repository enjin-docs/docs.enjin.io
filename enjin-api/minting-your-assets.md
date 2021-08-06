---
description: Learn more about Minting your Assets and NFTs
---

# Minting Your Assets

It's time to mint your first batch of assets. The request for minting Fungible Tokens \(FTs\) vs Non-Fungible Tokens \(NFTs\) varies slightly. You can mint batches of any token type to multiple addresses or mint them to a single address.

The supply of Fungible Tokens is essentially represented by a quantity field within the token data, as opposed to Non-Fungible Tokens whose supply is represented by the quantity of separate token identities.

If you need to mint multiple NFTs in a single transaction, you will need to specify the receiving Ethereum address for each individual item. It is also advisable not to mint over 150 NFTs in a single transaction.

FTs do not have the same restriction, you can mint unlimited Fungible Tokens to an Ethereum Address. However, it is advisable not to mint any amount of Fungible Tokens into over 100 different Ethereum Addresses in one transaction.

The following query will assist in Minting your Fungible and Non-Fungible Tokens.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  MintAsset(
    assetId: "708000000000088e"
    mints: { to: "WalletAddress", value: 1 }
    wallet: "WalletAddress"
    send: true
  ) {
    asset {
      name
      id
    }
    transactionId
    id
    value
    wallet {
      ethAddress
    }
  }
}
```
{% endtab %}
{% endtabs %}

### Cancelling Pending Transactions

If you are experiencing pending/stuck transactions on the Ethereum network, you can cancel a transaction using the following mutation: 

If the wallet daemon is complaining about a transaction with invalid parameters that need to be reverted, you can revert the transaction by using the following mutation:

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
    CancelTransaction(id: <transaction id here>)
}
```
{% endtab %}
{% endtabs %}

Note, it will be very rare to encounter any stuck transaction on JumpNet. If you do, however, try running the above mutation to cancel your stuck transaction. 

### Minting via Platform

You can also mint via the Enjin Platform on Mainnet or on JumpNet. Minting via the Enjin Platform is simple. 

1. First, locate the asset you want to mint, and click the `Mint` button on the far-right. 
2. Select the quantity to mint. 
3. Input an address that you'd like the asset\(s\) minted to. 

![](../.gitbook/assets/image%20%283%29.png)

> Note, minting via the Enjin Platform does have some limitations, such as you can only mint to 1 single address, rather than minting to multiple, unique addresses.



