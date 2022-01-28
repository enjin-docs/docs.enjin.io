---
description: A list of all Enjin Queries and Mutations for our latest v.2 schemas
---

# Enjin Queries & Mutations (V.2)

V.2 schemas are now available as a beta feature!

{% hint style="info" %}
You can enable v.2 schemas on your project (Mainnet, JumpNet or Kovan) by following this guide [here](https://enjin.io/help/v2-schemas-beta-release).&#x20;
{% endhint %}

### Enjin Queries

Querying is the way to ask for data, it’s similar to the GET action in REST-based APIs.

Here is a list of the Enjin object types you can query through the API:

* **AuthProject:** Use this query to obtain the unique access token of your project.
* **EnjinTokenEvent:** Use this to query the token events that have been recorded by the Enjin platform.
* **AuthPlayer:** Use this query to get the Access Token from a specific user.
* **GetBalances:** Use this query to get information about balances stored on the Enjin platform.
* **GetGasPrice:** Use this query to retrieve the latest gas prices.
* **GetWallet**: Use this query to retrieve information from a specific wallet.
* **GetWallets:** Use this query to retrieve information from multiple wallets.
* **GetPlatform:** Use this query to get information about the Platform.
* **GetPlayer:** Use this query to get information about your player on the Enjin platform.
* **GetPlayers:** Use this to query multiple players to retrieve information about them.
* **GetProject:** Use this query to get information about an app on the Enjin platform.
* **GetAsset:** Use this query to retrieve asset information.
* **GetAssets:** Use this query to retrieve information about multiple assets.
* **GetTransaction:** Use this to query transaction requests and their status.
* **GetTransactions:** Use this to query multiple transaction requests and their statuses.&#x20;

### Enjin Mutations

There are different types of Enjin object types that can be mutated through the API.

Here is a list of the Enjin object types that can be mutated:

* **AdvancedSendAsset:** Use this mutation to send one or more assets in a single transfer.
* **ApproveENJ:** Use this mutation to approve how much ENJ to spend.
* **CancelTransaction:** Use this mutation to cancel your transactions.
* **CompleteTrade:** Use this mutation to complete a trade between two wallets.
* **CreatePlayer:** Use this mutation to create your player in your integration.
* **CreateAsset:** Use this mutation to create your asset or NFT on your project.
* **CreateTrade:** Use this mutation to create a trade between two wallets.
* **DecreaseMaxMeltFee:** Use this mutation to set the max melt to an asset.
* **DecreaseMaxTransferFee:** Use this mutation to set the max transfer fee to an asset.
* **DeletePlayer:** Use this mutation to delete a player from your project.
* **InvalidateAssetMetadata:** Use this mutation to invalidate the cached asset metadata.
* **MeltAsset:** Use this mutation to melt an asset from your project.
* **Message:** Use this mutation to prove wallet ownership.
* **MintAsset:** Use this mutation to mint an asset from your project.
* **ReleaseReserve:** Use this mutation to release the asset reserve.&#x20;
* **SendENJ:** Use this mutation to send ENJ or JENJ.
* **SendAsset:** Use this mutation to send your assets to and from players.
* **SetApprovalForAll:** Use this mutation to allow an operator complete control on all assets.
* **SetUri:** Use this mutation to set asset metadata to your assets.
* **SetMeltFee:** Use this mutation to set a melt fee to your assets.
* **SetTransferFee:** Use this mutation to set a transfer fee to your assets.
* **SetTransferable:** Use this mutation to set a transferable option to your assets.
* **SetWhitelisted:** Use this mutation to set a whitelist option to your assets.
* **UnlinkWallet:** Use this mutation to unlink a wallet from your project.
* **UpdateName:** Use this mutation to update an asset name.&#x20;

You can find comprehensive information about what data can be queried and mutated using these Object Types in the [**GraphiQL Documentation Explorer**](https://jumpnet.cloud.enjin.io/graphql/playground)**.**

To find it, go to the [**GraphiQL visual interface**](https://jumpnet.cloud.enjin.io/graphql/playground) and click the `Docs` button on the sidebar.

### Querying Variables

You may notice in our documentation, we provide examples of our queries and mutations that you can use and they will often contain variables within them. You can query these variables by simply passing through the data in the `Query Variables` section at the bottom of the page.

Simply slide up the bottom bar (Query Variables) and begin inputting the variables and their respective data.

![](<../../.gitbook/assets/image (2).png>)

### Browsing the Schema

On the right side, there is the documentation panel to expand and browse for all the requests and parameters you can use. See [here](https://graphql.org/learn/queries/) for documentation on Queries and Mutations.&#x20;

### Making a Request

On the (top) left panel, you would enter in your request to be made to the Enjin Cloud. Press the `Play`button at the top to submit your request, and you will receive a response on the right panel. At times, a notification will appear in your wallet to sign a transaction depending on the request made.

_**Note:** You can now enable v.2 schemas on your project (Mainnet, JumpNet and/or Kovan). To do this, follow this guide_ [_here_](https://enjin.io/help/v2-schemas-beta-release)_._
