---
description: Find all of the requests that can be run by a Project
---

# Project

## Queries

### AuthProject

Use this query to obtain an access asset for your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query GetAccessToken {
  AuthProject(uuid: <string>, secret: "appsecret"){
    accessToken
    expiresIn
  }
}
```
{% endtab %}
{% endtabs %}

### AuthPlayer

Use this query to obtain an access asset for a player.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query GetPlayerAccessToken {
  AuthPlayer(id: "TassinhoUser"){
    accessToken
    expiresIn
  }
}
```
{% endtab %}
{% endtabs %}

### **GetProject**

Use this query to get information about your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
{
  GetProject {
    uuid
    name
    description
    image
    createdAt
    updatedAt
  }
}
```
{% endtab %}
{% endtabs %}

### GetPlayer + GetPlayers

Use this query to get information about one of your players.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetPlayers {
    id
    wallet { 
      ethAddress
    }
    linkingInfo {
      code
      qr
    }
    createdAt
    updatedAt
  }
}
```
{% endtab %}
{% endtabs %}

### GetBalances

Use this query to get information about balances within your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetBalances {
    items {
      id
      index
      value
    }
  }
}
```
{% endtab %}
{% endtabs %}

### GetGasPrice

Use this query to get the latest gas prices.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
{
  GetGasPrice {
    fast
    fastest
    safeLow
    average
  }
}
```
{% endtab %}
{% endtabs %}

### GetPlatform

Use this query to get information about the Platform.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetPlatform {
    id
    name
    network
    contracts {
      enj
      cryptoItems
      platformRegistry
      supplyModels {
        fixed
        settable
        infinite
        collapsing
        annualValue
        annualPercentage
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

### GetTransaction + GetTransactions

Use this to query a transaction.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetTransaction(id:31179) {
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
{% endtab %}
{% endtabs %}

### GetWallet + GetWallets

Get a player wallet from an eth address or user id.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetWallet(ethAddress: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406") {
    ethAddress
    enjAllowance
    enjBalance
    ethBalance
    balances {
      asset{name}
      id
      index
      value
      project {
        name
      }
    }
    assetsCreated {
      id
      items {
        name
        id
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

### GetAsset + GetAssets

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetAsset(id: "708000000000088e") {
    id
    name
    createdAt
    updatedAt
    wallet {
      ethAddress
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Mutations

### **AdvancedSendAsset**

Send one or more assets in one transaction.

{% tabs %}
{% tab title="GraphQL" %}
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
{% endtab %}
{% endtabs %}

### **ApproveENJ**

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  ApproveEnj(
    value: "0"
    wallet: "WalletAddress"
  ) {
    type
    value
    state
  }
}
```
{% endtab %}
{% endtabs %}

### **ApproveMaxENJ**

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  ApproveMaxEnj(
    wallet: "WalletAddress"
  ) {
    type
    value
    state
  }
}
```
{% endtab %}
{% endtabs %}

### **CancelTransaction**

Use this mutation to cancel a transaction.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  CancelTransaction(id: 160538)
}
```
{% endtab %}
{% endtabs %}

### **CompleteTrade**

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  CompleteTrade(
    tradeId: "160502"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### **CreateTrade**

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  CreateTrade(
    askingAssets: [{ assetId: "784000000000033b", value: 1 }]
    offeringAssets: [
      { assetId: "70c0000000000005", value: 1, assetIndex: "0000000000000002" }
    ]
    secondParty: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### **CreateAsset**

Create an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  CreateAsset(
    name: "Test"
    totalSupply: "1"
    initialReserve: "1"
    supplyModel: COLLAPSING
    meltValue: "1000000000000000000"
    meltFeeRatio: 0
    transferable: PERMANENT
    transferFeeSettings: {type:PER_TRANSFER, assetId: "0", value: "0" }
    nonFungible: true
    wallet: "WalletAddress"
  ) {
    value
    id
    transactionId
    title
    state
    project{name}
  }
}
```
{% endtab %}
{% endtabs %}

### **CreatePlayer**

Use this mutation to create a player of your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  CreatePlayer(id: "BOB") {
    accessToken
  }
}
```
{% endtab %}
{% endtabs %}

### DeletePlayer

Use this mutation to delete a player from your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  DeletePlayer(id: "BOB")
}
```
{% endtab %}
{% endtabs %}

### DecreaseMaxMeltFee

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  DecreaseMaxMeltFee(
    assetId: "38400000000004cd"
    maxMeltFee: 2500
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### DecreaseMaxTransferFee

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  DecreaseMaxTransferFee(
    assetId: "58400000000004ce"
    maxTransferFee: "0"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### InvalidateAssetMetadata

Use this mutation to invalidate the cached asset metadata.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation InvalidateTokenMetadata {
  InvalidateAssetMetadata(id: "<tokenId>")
}
```
{% endtab %}
{% endtabs %}

### MeltAsset

Melt an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  MeltAsset(
  melts:[{assetId:"58400000000004ce",value:"1"}]
    wallet:"0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### Message

Sign a message to prove wallet ownership.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  Message(
    message:"This is a Test"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    type
    value
    state
  }
}
```
{% endtab %}
{% endtabs %}

### MintAsset

Mint an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  MintAsset(
    assetId: "708000000000088e"
    mints: { to: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406", value: 1 }
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
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

### MintAsset #2

Mint 1x asset to various addresses.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation mintAssets {
  MintAsset(
    wallet: "0x0"
    assetId: "70c0000000000e22"
    mints: [
      { to: "0x787b5DAcbc42171eD6c1b107B85d4C8D94380a3e", value: 1 }
      { to: "0x22523b285Bf97a099F5C874f920D7c3229Bab963", value: 1 }
      { to: "0xc4Ef6992136FFE977e42133321f8a4aFB178b5be", value: 1 }
    ]
  ) {
    id
  }
}
```
{% endtab %}
{% endtabs %}

### ReleaseReserve

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
 ReleaseReserve(
  assetId: "70c00000000003b2"
  value: "3"
  wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SendENJ or JENJ

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SendEnj(
    to: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
    value: "100000000000000000"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
  }
}
```
{% endtab %}
{% endtabs %}

### SendAsset

Send an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SendAsset(
    assetId: "78c00000000004b1"
    assetIndex: "0000000000000001"
    to: "0xc18de03b63ab13b1bf6b146003d029c64bc17514"
    value: "1"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetApprovalForAll

Allow an operator complete control on all assets owned by caller.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetApprovalForAll(
    operator: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
    approved: true
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetUri

Set the asset metadata uri.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetUri(
    assetId: "78c00000000004b1"
    uri:"https://cdn.enjin.io/mint/meta/70c0000000000469.json"
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetMeltFee

Set the melt fee of an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetMeltFee(
    assetId: "38c0000000000516"
    meltFee: 500
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetTransferFee

Set the transfer fee of an asset.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetTransferFee(
    assetId: "584000000000000b"
    transferFee: 1000000000000000
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetTransferable

Set if an asset can be transferred or not.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetTransferable(
    assetId: "6840000000000531"
    transferable: BOUND
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### SetWhitelisted

Set the asset whitelist.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
  SetWhitelisted(
    assetId:"78c00000000004b1"
    account:"0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
    whitelisted:SEND_AND_RECEIVE
    on:true
    wallet: "0x7AEAB7C231c88611a2ad434d3A2715Ab3C91F406"
  ) {
    transactionId
    id
    state
    value
    asset {
      name
      id
    }
    user {
      name
    }
  }
}
```
{% endtab %}
{% endtabs %}

### UnlinkWallet

Use this mutation to unlink a wallet from your app.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation project {
  UnlinkWallet(address: "<wallet address here>")  
}
```
{% endtab %}
{% endtabs %}

