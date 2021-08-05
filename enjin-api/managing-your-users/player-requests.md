# Player Requests

### Unlinking a Wallet

At times, your user may want to change wallets, which they can do this via the Enjin Wallet by going to the "Linked Apps" section, tapping on the project, tap on the 3-dot menu and select "Delete".  
Additionally, you can also initiate this on your end.

The following query will unlink their wallet and allow them to re-link it, or link a new one:

```graphql
mutation UnlinkWalletAddress($id: Int!) {
 DeleteEnjinIdentity(id: $id, unlink: true) {
   linkingCode
   linkingCodeQr
 }
}
```

### Viewing Tokens in a Wallet

Once a player is logged in and linked, the first thing you will want to do is see their inventory so you can provide them with game items to match their tokens.

It's advisable to update the user's balance on your database. That way, your project or game can run efficiently on the data you are holding.

```graphql
query getBalance($address: String!) {
 EnjinBalances(ethAddress: $address, value_gt: 0) {
   token {
     id
     index
     name
   }
   value
 }
}
```

It's important to include the `value_gt: 0` argument because it prevents the display of melted items. They technically still exist within that blockchain address, even though the user has chosen to destroy/melt them.

### View Specific Tokens in a Wallet

When you want to perform a specific action with a token, you can use this to validate whether the token is still there.

```graphql
query GetWalletTokenBalance($address: String!, $tokenId: String) {
 EnjinBalances(ethAddress: $address, tokenId: $tokenId, value_gt: 0) {
   token {
     id
     index
     name
   }
   value
 }
}
```

This query displays the token index and balance of the token in question.

You can also choose to request the data for `tokenId` and `id` by adding the fields to the query.

### View ENJ Balance

You can view the amount of Enjin Coin \(ENJ\) or JumpNet ENJ \(JENJ\) of a user in the wallet. This can be useful, if you need to know if they have enough Enjin Coin to approve certain transactions and requests. You can use the following query to retrieve the ENJ balance:

```graphql
query GetWalletBalance($id: Int!) {
 EnjinUsers(id: $id) {
   identities {
     wallet {
       ethAddress
       enjBalance
     }
   }
 }
}
```

If you don't know the user ID or the Identity ID, you can use the following query to retrieve the same results, simply with the Ethereum address instead:

```graphql
query GetWalletBalanceByAddress($address: String!) {
 EnjinWallet(ethAddress: $address) {
   enjBalance
   ethBalance
 }
}
```

