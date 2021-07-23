---
description: Learn how you can get started
---

# Using GraphQL

GraphQL is a modern query language that allows you to define the data structure of your queries and ask for exactly what you want and nothing more.

GraphQL queries access not just the properties of one resource but also smoothly follow references between them. While typical REST APIs require loading from multiple URLs, GraphQL APIs get all the data your app needs in a single request.

### Operations

**Query:** READ operations are performed by GraphQL queries, these do not change data.

**Mutation:** You will use mutations to perform all other operations to modify data.

### Object Types

Object types are sets of fields that are used to define the set of data you can query from the API.

{% tabs %}
{% tab title="V1" %}
query { 

}

mutation { 

}
{% endtab %}

{% tab title="V2" %}
query { 

}

mutation { 

}
{% endtab %}
{% endtabs %}

```graphql
query {

}

mutation {

}
```

### Fields

Fields are used to ask for specific object properties.

Each object has fields that can be queried by name in order to query for the properties you need.

{% tabs %}
{% tab title="V1" %}
```graphql
query GetToken($name: String) {
token: EnjinTokens(
  name: $name
) {
  id
}
}
```
{% endtab %}

{% tab title="v2" %}
```graphql
query {
 EnjinToken {
    id
 }
}
```
{% endtab %}
{% endtabs %}

### Arguments

You can determine the return value of a query by passing arguments to it. This narrows down the results and allows you to only get what you're after.

In the following example, the object is “token”, the requested field is “name”, the argument is “id”.

{% tabs %}
{% tab title="GraphQL" %}
```graphql
query GetToken($name: String) {
token: EnjinTokens(
  name: $name
) {
  id
}
}
```
{% endtab %}
{% endtabs %}

