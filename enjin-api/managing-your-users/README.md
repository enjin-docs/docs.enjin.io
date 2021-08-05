# Managing Your Users

### Creating a User

In this step, with the access token that you retrieved in the previous step, you will need to pass that as the authorization header when performing the `createUser` mutation.

Your authorization system needs to check to see if a user's account has been created yet.

* If it hasn't, it should create a new account for them.
* If it has, then the system should try to log them in.

The following query will create a new user for your system:

```graphql
mutation CreateUser($name: String!) {
 CreateEnjinUser(name: $name) {
   id
   accessTokens
   identities {
     linkingCode
     linkingCodeQr
     wallet {
       ethAddress
     }
   }
 }
}
```

Once you have created an Enjin account, it's advisable to enter the reference into your database, so you don't repeat this process unnecessarily in the future.

### Loggin Your User In

In this final step of integration, once you are have confirmed that your user has an existing account, you can log your user in by following this query:

```graphql
query RetrievePlayerAccessToken($name: String!) {
 AuthPlayer(id: $name) {
   accessToken
   expiresIn
 }
}
```

If the API returns a linking code, that means the user's Enjin Wallet is not linked. If no linking code is returned, this means the wallet is linked and you can send the user into the game.



