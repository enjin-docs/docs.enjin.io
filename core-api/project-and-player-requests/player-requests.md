---
description: Find all of the requests that can be run by a Player
---

# Player

## Queries

### GetAsset + GetAssets

Use this to query assets.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query {
  GetAsset(id: "tokenId") {
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

### GetBalances

Use this to query the player's asset balances.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query{
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

### GetPlayer

Use this query to get information about the player.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
{
  GetPlayer(id: "yourUserName") {
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

### GetProject

Use this query to get information about your app.

```
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

### GetTransaction + GetTransactions

Use this to query a transaction broadcast by the player.

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

### GetWallet

Get the wallet for the player.

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

## Mutations

### AdvancedSendAsset

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

### CancelTransaction

Use this mutation to cancel a transaction.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation {
    CancelTransaction(id: <id here>)
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

### SendENJ or JENJ

Send ENJ.

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
    operator: "address here"
    approved: true
    wallet: "address here"
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
