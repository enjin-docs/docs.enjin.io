---
description: Learn more about how to set-up trading in your integration
---

# Trade Requests

You can also initiate certain trade requests in your project, to allow your players to freely trade between themselves different assets they own.

### Step 1: Send Trade Request

Initiate a send trade request using the following mutation:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation SendTradeRequest($initiatorId: Int!, $recipientId: Int!) {
  CreateEnjinRequest(
    identityId: $initiatorId
    type: CREATE_TRADE
    create_trade_data: {
      asking_tokens: [{ id: "XXXXXXXXXXXXXXXXX", value: 1 }]
      offering_tokens: [{ id: "XXXXXXXXXXXXXXXXX", value: 1 }]
      second_party_identity_id: $recipientId
    }
  ) {
    id
    encodedData
    state
  }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

### **Step 2:** Get the Trade ID

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query RetrieveTradeId($id: Int!) {
  EnjinTransactions(id: $id) {
    type
    transactionId
    events {
      param1
    }
  }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

### **Step 3:** Complete the trade request

Enter param1 as `trade_id`, 2nd person `identity_id`, and confirm in the 2nd person's wallet.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation CompleteTradeRequest($id: Int!, $tradeId: String!) {
  CreateEnjinRequest(
    identity_id: $id
    type: COMPLETE_TRADE
    complete_trade_data: { trade_id: $tradeId }
  ) {
    id
    transactionId
    encodedData
  }
}
```
{% endtab %}
{% endtabs %}

