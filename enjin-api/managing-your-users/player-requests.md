---
description: Learn additional requests that you can do with the your integration
---

# Additional Requests

### Unlinking a Wallet

At times, your user may want to change wallets, which they can do via the Enjin Wallet by going to the "Linked Projects" section, tapping on the project, tapping on the 3-dot menu and selecting "Delete". 

Additionally, you can also initiate this on your end.

The following query will unlink their wallet, allow them to re-link it, or link with a new one:

```graphql
mutation project {
  UnlinkWallet(address: "<address here>")  
}
```

### Viewing Assets in a Wallet

Once a player is logged in and linked, the first thing you will want to do is see their inventory so you can provide them with game items to match their assets.

It's advisable to update the user's balance on your database. That way, your project or game can run efficiently on the data you are holding.

You can also view the ENJ balance, ETH balance and their ETH address when running this query. 

```graphql
query {
  GetWallet(ethAddress: "User's Address") {
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

