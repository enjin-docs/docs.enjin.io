---
description: A list of all Enjin Queries and Mutations for our latest v.2 schemas
---

# Enjin Queries & Mutations \(V.2\)

### Enjin Queries

Querying is the way to ask for data, it’s similar to the GET action in REST-based APIs.

Here is a list of the Enjin object types you can query through the API:

* **GetProject:** Use this query to get information about an app on the Enjin platform.
* **AuthProject:** Use this query to obtain the unique access token of your project.
* **AuthPlayer:** Use this query to get the Access Token from a specific user.
* **GetBalances:** Use this query to get information about balances stored on the Enjin platform.
* **GetGasPrice:** Use this query to retrieve the latest gas prices.
* **GetWallet**: Use this query to retrieve information from a specific wallet.
* **GetWallets:** Use this query to retrieve information from multiple wallets.
* **EnjinTokenEvent:** Use this to query the token events that have been recorded by the Enjin platform.
* **GetPlatform:** Use this query to get information about the Platform.
* **GetPlayer:** Use this query to get information about your player on the Enjin platform.
* **GetPlayers:** Use this to query multiple players to retrieve information about them.
* **GetAsset:** Use this query to retrieve asset information.
* **GetAssets:** Use this query to retrieve information about multiple assets.
* **GetTransaction:** Use this to query transaction requests and their status.
* **GetTransactions:** Use this to query multiple transaction requests and their statuses. 

### Enjin Mutations

There are different types of Enjin object types that can be mutated through the API.

Here is a list of the Enjin object types that can be mutated:

* **ApproveENJ:** Use this mutation to approve how much ENJ to spend.
* **CancelTransaction:** Use this mutation to cancel your transactions.
* **CreatePlayer:** Use this mutation to create your player in your integration.
* **DeletePlayer:** Use this mutation to delete a player from your project.
* **InvalidateAssetMetadata:** Use this mutation to invalidate the cached asset metadata.
* **UnlinkWallet:** Use this mutation to unlink a wallet from your project.
* **AdvancedSendAsset:** Use this mutation to send one or more assets in a single transfer.
* **CompleteTrade:** Use this mutation to complete a trade between two wallets.
* **CreateAsset:** Use this mutation to create your asset or NFT on your project.
* **CreateTrade:** Use this mutation to create a trade between two wallets.
* **DecreaseMaxMeltFee:** Use this mutation to set the max melt to an asset.
* **DecreaseMaxTransferFee:** Use this mutation to set the max transfer fee to an asset.
* **MeltAsset:** Use this mutation to melt an asset from your project.
* **Message:** Use this mutation to prove wallet ownership.
* **MintAsset:** Use this mutation to mint an asset from your project.
* **ReleaseReserve:** Use this mutation to release the asset reserve. 
* **SendENJ:** Use this mutation to send ENJ or JENJ.
* **SendAsset:** Use this mutation to send your assets to and from players.
* **SetApprovalForAll:** Use this mutation to allow an operator complete control on all assets.
* **SetUri:** Use this mutation to set asset metadata to your assets.
* **SetMeltFee:** Use this mutation to set a melt fee to your assets.
* **SetTransferFee:** Use this mutation to set a transfer fee to your assets.
* **SetTransferable:** Use this mutation to set a transferable option to your assets.
* **SetWhitelisted:** Use this mutation to set a whitelist option to your assets.
* **UpdateName:** Use this mutation to update an asset name. 

You can find comprehensive information about what data can be queried and mutated using these Object Types in the [**GraphiQL Documentation Explorer**](https://jumpnet.cloud.enjin.io/graphql/playground)**.**

To find it, go to the [**GraphiQL visual interface**](https://jumpnet.cloud.enjin.io/graphql/playground) and click the `Docs` button on the sidebar.

