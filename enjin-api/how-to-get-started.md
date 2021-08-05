---
description: Learn how to get set-up and start using the Enjin API
---

# How to Get Started

As you start, it's **very important** that all of your admin and user data is parsed and stored by a secure server.

This means ****you will need solid knowledge of our Cloud API \(GraphQL\) to complete your secure integration.

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

> **NOTE: MAKE SURE TO STORE THIS SERVERSIDE!**

Once you have retrieved the app secret from the previous step, you will need the access token, which you can retrieve by following this query:

```graphql
query RetrieveAppAccessToken($appId: Int!, $appSecret: String!) {
 AuthApp(id: $appId, secret: $appSecret) {
   accessToken
   expiresIn
 }
}
```



