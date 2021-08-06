---
description: Start manging your players with your integration
---

# Managing Your Players

### Step 1: Creating a Player

In this step, with the access token that you retrieved in the previous step, you will need to pass that as the authorization header when running the `CreatePlayer` mutation.

Your authorization system needs to check to see if a user's account has been created yet.

* If it hasn't, it should create a new account for them.
* If it has, then the system should try to log them in.

The following query will create a new player for your system:

```graphql
mutation {
  CreatePlayer(id: "John Wick") {
    accessToken
  }
}
```

Once you have created an Enjin account, it's advisable to enter the reference into your database, so you don't repeat this process unnecessarily in the future.

### Step 2: Loggin Your Player In

In this final step of integration, once you are have confirmed that your player has an existing account, you can log your player in by following this query:

```graphql
query GetPlayerAccessToken {
  AuthPlayer(id: "John Wick"){
    accessToken
    expiresIn
  }
}
```

To check if your player has linked their Enjin Wallet, you can run the following query:

```graphql
{
  GetPlayer(id: "John Wick") {
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

If the API request returns a valid linking code and/or linking QR link, then your player hasn't linked their wallet. If there's no linking code \(i.e. displaying `null`\), this means the wallet is linked and you can send your player into your game.



