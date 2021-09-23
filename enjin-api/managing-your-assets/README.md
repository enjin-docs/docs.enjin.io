---
description: Learn more about how to manage your NFTs within your integration
---

# Managing Your Assets

The Enjin API has been built to provide all the functionality you need to manage a robust blockchain-based gaming economy.

You will likely use the following queries and mutations quite often when it comes to managing your tokenized assets in your project or in your game. 

Some of these requests involves managing your assets in different ways to customise the experience how you want your NFTs to work in your integration. 

## Change Asset Name

Assets have their names specified on the blockchain and within their metadata. This means assets can, technically, be given a different name on the blockchain and in its metadata.

The following mutation can be used to update a token's name on the blockchain:

```graphql
mutation UpdateTokenName($identityId: Int!, $itemNameData: UpdateItemNameInput!) {
 CreateEnjinRequest(identityId: $identityId, type: UPDATE_NAME, update_item_name_data: $itemNameData) 
 {
   id
   encodedData
 }
}
```

## Melt Batch Items

There may be times that you make a mistake during the asset minting process and you wish to melt all of the assets you have created.

To melt any asset, the asset must be in your wallet. It's important to **quadruple-check** your token settings prior to sending them to your users.

Once your assets have been distributed to your users, there is no going back and the only way to fix any errors is to generate replacement tokens.

```graphql
mutation BatchMelt($identityId: Int!, $meltTokenData: MeltTokenInput!) {
 CreateEnjinRequest(identityId: $identityId, type: MELT, melt_token_data: $meltTokenData) {
   identityId
   tokenId
 }
}
```

## Release Reserve

When you first create an asset, you will be asked to lock an initial reserve on the Enjin Coin \(ENJ\) into it.

This is to ensure you can mint your tokens fluidly, using the Enjin Coin you have set aside.

If you no longer wish to use the asset and decide not to go ahead with minting the respective tokens, you can destroy the asset and return the Enjin Coin that you have set aside. You can do that by using the following mutation:

```graphql
mutation ReleaseReserve($identityId: Int!, $tokenId: String!, $value: Int!) {
 CreateEnjinRequest(identityId: $identityId, type: RELEASE_RESERVE, release_reserve_data: {token_id: $tokenId, value: $value}) {
   tokenId
 }
}
```

{% hint style="warning" %}
There is a cool-down period for releasing reserve and the more Enjin Coin you have locked into the template, the longer you have to wait until you can release it. This waiting period can take days or even weeks.
{% endhint %}

## Send All Item Types: Advanced Send

The Platform API allows you to send an unlimited amount of Fungible tokens and up to 100 Non-Fungible tokens to up to 1000 users, in a single transaction. The Advanced Send mutation is one of the most common mutations to send vast amounts of assets from one address to another in a single transaction and with ease.

This is the most robust and popular sending mutation used by developers:

```graphql
mutation AdvancedSend($identityId: Int!, $tokenData: AdvancedSendTokenInput!) {
 CreateEnjinRequest(identityId: $identityId, type: ADVANCED_SEND, advanced_send_token_data: $tokenData) {
   id
   encodedData
 }
}
```

## Transfer Whitelisting

If you've created a bound token or a token with transfer fees, and you don't wish for these settings to apply in every circumstance, you can use transfer whitelisting to allow specific users to send tokens to specific addresses.

```graphql
mutation WhitelistToken($identityId: Int!, $appId: Int!, $whitelistData: SetWhitelistedInput!) {
 CreateEnjinRequest(identityId: $identityId, appId: $appId, type: SET_WHITELISTED, set_whitelisted_data: $whitelistData) {
   id
   encodedData
 }
}
```

### Whitelist Settings

**Full Rights:** The address has full rights to send and receive the token.  
`0x0000000000000000000000000000000000000001`

**Can Send:** The address can send but not receive the token. Which means that the only way they can get the token, is if you mint it directly to their address.  
`0x0000000000000000000000000000000000000002`

**Can Receive:** The address can receive but can't send the token.  
`0x0000000000000000000000000000000000000003`

**No Fees:** The address can send tokens without paying transfer fees.  
`0x0000000000000000000000000000000000000004`

## Asset Details, Holders & Transaction Data

If you wish to provide your users with detailed information about a specific asset, you can use this query to look up the data:

```graphql
query GetTokenDetails($name: String!) {
 EnjinTokens(name: $name, pagination: {page: 1, limit: 50}) {
   id
   name
   creator
   meltValue
   meltFeeRatio
   meltFeeMaxRatio
   supplyModel
   totalSupply
   circulatingSupply
   reserve
   transferable
   nonFungible
   blockHeight
   markedForDelete
   createdAt
   updatedAt
   availableToMint
   itemURI
 }
}
```

### Token Holders

This query returns a list of addresses who own a specific token:

```graphql
query GetBalance($tokenId: String!) {
 EnjinBalances(tokenId: $tokenId) {
   token {
     id
     index
   }
   wallet {
     ethAddress
   }
   value
 }
}
```

It can be useful for rewarding all holders of a specific token in one go, through a coordinated airdrop.

### Transaction Data

Whenever you issue a send mutation, a transaction id will be returned to you. This id is very important and it is highly advisable to log this data so you can access it again, at a later date.

Should you want to view the state of any transaction that you have performed on the blockchain, you will need to use this query:

```graphql
query GetTransaction($id: Int!) {
 EnjinTransactions(id: $id) {
   id
   transactionId
   type
   state
   error
   token {
     id
     name
   }
 }
}
```

The Enjin Transactions query will return various pieces of information, depending on the state of the transaction that you have run.

  
You will notice that we added the `error` argument within the query. The `error` argument is useful to have, in case your transaction has failed/dropped for a certain reason. This will display why the transaction did not process on the network.

This query will return the following values:

* **PENDING:** Transaction is created on the Enjiin Cloud, but has not yet been signed by the user/dev.
* **TP\_PROCESSING:** Transaction has been signed and is waiting for the Enjin Cloud/Platform\) to process the transaction for broadcast.
* **BROADCAST:** Transaction has been signed and has been broadcast but has not yet been confirmed on the blockchain.
* **EXECUTED:** The transaction has received confirmation on the blockchain and the Enjin Cloud.
* **CANCELED\_USER:** The user has cancelled the PENDING transaction/not signed.
* **CANCELED\_PLATFORM:** The Platform has cancelled the PENDING transaction.
* **FAILED:** Transaction has failed on the Enjiin Platform.
* **DROPPED:** Transaction was not mined on the blockchain and has since been dropped.

## Set Spending Allowance

If you want to increase the security of your project and set a spending limit for yourself, or allow your players to choose their own spending limits, you can use this mutation to set a spending allowance:

```graphql
mutation ApproveEnj($id: String!, $limit: Int!) {
  CreateEnjinRequest(
    identityId: $id
    type: APPROVE
    approve_enj_data: { value: $limit }
  ) {
    id
  }
}
```

Set value as -1 for **max** value.

{% hint style="info" %}
This value decreases as it is used, like a literal spending allowance. If you set the value to 10 Enjin Coin \(ENJ\) and then make 10 transactions for 1 ENJ each, your allowance will go down to 0 and it will need to be set again.
{% endhint %}

## Changing Asset Transfer Status

At times, you may want to change the transfer status of an asset that you've created to give it a certain value, whether you want the asset to be **permanently transferable**, **temporarily transferable**, or **bound** to an address.

The following mutation will allow you to change the asset transferable type:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation ChangeAssetTransferableType(
  $appId: Int!
  $identityId: Int!
  $tokenId: String!
  $transferable: TokenTransferable!
) {
  CreateEnjinRequest(
    appId: $appId
    identityId: $identityId
    type: SET_TRANSFERABLE
    set_transferable_data: { token_id: $tokenId, transferable: $transferable }
  ) {
    id
    encodedData
  }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```


```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
If you set the token to be permanently transferable, you will not be able to alter that setting.
{% endhint %}

