---
description: >-
  Getting Started with the Enjin API. Learn how to manage your players, send and
  receive assets, set metadata, mint your assets and manage them.
---

# Getting Started

As you start, it's **very important** that all of your admin and user data is parsed and stored by a secure server.

This means ****you will need a solid understanding of our Cloud API \(GraphQL\) to complete your secure integration. 

If you haven't, we recommend going through the section "What is GraphQL?" and taking a look at our directory of all the available GraphQL queries and mutations to use:

{% page-ref page="../core-api/using-graphql/graphql-visual-interface.md" %}

### Step 1: Getting Your Bearer Token

The first step is acquiring your bearer token. You can log into your account via our API using the following query:

```graphql
query Login($email: String!, $password: String!) {
 EnjinOauth(email: $email, password: $password) {
   id
   name
   accessTokens
 }
}
```

### Step 2: Getting Your Secret Key

You will need to acquire your secret key by following this query:

```graphql
query GetAppSecret($id: Int!) {
 EnjinApps(id: $id){
   secret
 }
}
```

### Step 3: Getting Your Access Token

Once you have retrieved the app secret from the previous step, you will need the access token, which you can retrieve by following this query:

{% hint style="danger" %}
**IMPORTANT:** Make sure to store your access token serverside!
{% endhint %}

```graphql
query RetrieveAppAccessToken($appId: Int!, $appSecret: String!) {
 AuthApp(id: $appId, secret: $appSecret) {
   accessToken
   expiresIn
 }
}
```



