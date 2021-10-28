# Viewing a Player's NFTs

## Goal

To view the contents of a user's verified wallet, which will then allow you to provide benefits and content based on which NFTs they own.

## Process

When users want to access your content, you need to check what items are in their wallet with the following code:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query getBalance {
   EnjinBalances (
        ethAddress: "<Ethereum Address>",
        value_gte: 1,
        appIds: [<App ID>]
    ) {
     token {
        id
        name
        itemURI
        meltValue
      }
      index
      value
  }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

