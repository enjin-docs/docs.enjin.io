# Managing Your Assets

Once your tokens have been minted, you may want to edit, send, or melt them down and recover the Enjin Coin \(ENJ\) from within inside the tokens.

The Platform API has been built to provide all the functionality you need to manage a robust blockchain-based gaming economy.

You will likely use the following queries and mutations quite often when it comes to managing your tokenized assets.

## Change Token Name

Tokens have their names specified on the blockchain and within their metadata.

This means tokens can, technically, be given a different name on the blockchain and in its metadata.

The following mutation can be used to update a token's name on the blockchain:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation UpdateTokenName($identityId: Int!, $itemNameData: UpdateItemNameInput!) {
 CreateEnjinRequest(identityId: $identityId, type: UPDATE_NAME, update_item_name_data: $itemNameData) 
 {
   id
   encodedData
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## Melt Batch Items

There may be times that you make a mistake during the token minting process and you wish to melt all of the tokens you have created.

To melt any token, the token must be in your wallet. It's important to **quadruple-check** your token settings prior to sending them to your users.

Once your tokens have been distributed to your users, there is no going back and the only way to fix any errors is to generate replacement tokens.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation BatchMelt($identityId: Int!, $meltTokenData: MeltTokenInput!) {
 CreateEnjinRequest(identityId: $identityId, type: MELT, melt_token_data: $meltTokenData) {
   identityId
   tokenId
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## Release Reserve

When you first create a token, you will be asked to lock an initial reserve on the Enjin Coin \(ENJ\) into it.

This is to ensure you can mint your tokens fluidly, using the Enjin Coin you have set aside.

If you no longer wish to use the token and decide not to go ahead with minting the respective tokens, you can destroy the template and return the Enjin Coin that you have set aside by using the following mutation:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation ReleaseReserve($identityId: Int!, $tokenId: String!, $value: Int!) {
 CreateEnjinRequest(identityId: $identityId, type: RELEASE_RESERVE, release_reserve_data: {token_id: $tokenId, value: $value}) {
   tokenId
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

_**Note:**_ There is a cool-down period for releasing reserve and the more Enjin Coin you have locked into the template, the longer you have to wait until you can release it. This waiting period can take days or even weeks.

## Send All Item Types: Advanced Send

The Platform API allows you to send unlimited Fungible and up to 100 Non-Fungible tokens to up to 1000 users, in a single transaction. The Advanced Send mutation is one of the most common mutations to send vast amounts of assets from one address to another in a single transaction and with ease.

This is the most robust and popular sending mutation used by developers:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation AdvancedSend($identityId: Int!, $tokenData: AdvancedSendTokenInput!) {
 CreateEnjinRequest(identityId: $identityId, type: ADVANCED_SEND, advanced_send_token_data: $tokenData) {
   id
   encodedData
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## Transfer Whitelisting

If you've created a bound token or a token with transfer fees, and you don't wish for these settings to apply in every circumstance, you can use transfer whitelisting to allow specific users to send tokens to specific addresses.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation WhitelistToken($identityId: Int!, $appId: Int!, $whitelistData: SetWhitelistedInput!) {
 CreateEnjinRequest(identityId: $identityId, appId: $appId, type: SET_WHITELISTED, set_whitelisted_data: $whitelistData) {
   id
   encodedData
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

### Whitelist Settings

**Full Rights:** The address has full rights to send and receive the token.  
`0x0000000000000000000000000000000000000001`

**Can Send:** The address can send but not receive the token. Which means that the only way they can get the token, is if you mint it directly to their address.  
`0x0000000000000000000000000000000000000002`

**Can Receive:** The address can receive but can't send the token.  
`0x0000000000000000000000000000000000000003`

**No Fees:** The address can send tokens without paying transfer fees.  
`0x0000000000000000000000000000000000000004`

## Token Details

If you wish to provide your users detailed information about a specific token, you can use this query to look up the data:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query GetTokenDetails($name: String!) {
 EnjinTokens(name: $name, pagination: {page: 1, limit: 50}) {
   id
   name
   creator
   meltValue
   meltFeeRatio
   meltFeeMaxRatio
   supplyModel
   totalSupply
   circulatingSupply
   reserve
   transferable
   nonFungible
   blockHeight
   markedForDelete
   createdAt
   updatedAt
   availableToMint
   itemURI
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## Token Holders

This query returns a list of addresses who own a specific token:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query GetBalance($tokenId: String!) {
 EnjinBalances(tokenId: $tokenId) {
   token {
     id
     index
   }
   wallet {
     ethAddress
   }
   value
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

It can be useful for rewarding all holders of a specific token in one go, through a coordinated airdrop.

## Transaction Data

Whenever you issue a send mutation, a transaction id will be returned to you. This id is very important and it is highly advisable to log this data so you can access it again, at a later date.

Should you want to view the state of any transaction that you have performed on the blockchain, you will need to use this query:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query GetTransaction($id: Int!) {
 EnjinTransactions(id: $id) {
   id
   transactionId
   type
   state
   error
   token {
     id
     name
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



The Enjin Transactions query will return various pieces of information, depending on the state of the transaction that you have run.  
You will notice that we added the error argument within the query. The error argument is useful to have, in case your transaction has failed/dropped for a certain reason, this will display why the transaction in question did not process on the blockchain.

**This query will return the following values:**

* **PENDING:** Transaction is created on the Enjiin Cloud, but has not yet been signed by the user/dev.
* **TP\_PROCESSING:** Transaction has been signed and is waiting for the Enjin Cloud/Platform\) to process the transaction for broadcast.
* **BROADCAST:** Transaction has been signed and has been broadcast but has not yet been confirmed on the blockchain.
* **EXECUTED:** The transaction has received confirmation on the blockchain and the Enjin Cloud.
* **CANCELED\_USER:** The user has canceled the PENDING transaction/not signed.
* **CANCELED\_PLATFORM:** The Platform has canceled the PENDING transaction.
* **FAILED:** Transaction has failed on the Enjiin Platform.
* **DROPPED:** Transaction was not mined on the blockchain and has since been dropped.

## Set Spending Allowance

If you want to increase the security of your project and set a spending limit for yourself, or allow your players to choose their own spending limits, you can use this mutation to set a spending allowance:

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation ApproveEnj($id: String!, $limit: Int!) 
{CreateEnjinRequest(identityId: $id, type: APPROVE, 
approve_enj_data: {value: $limit}) {id}}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

Set value as -1 for **max** value.

_**Note:**_ This value decreases as it is used, like a literal spending allowance. If you set the value to 10 Enjin Coin \(ENJ\) and then make 10 transactions for 1 ENJ each, your allowance will go down to 0 and it will need to be set again.

## Trade Request

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation SendTradeRequest($initiatorId: Int!, $recipientId: Int!) {
 CreateEnjinRequest(identityId: $initiatorId, type: CREATE_TRADE, create_trade_data: {asking_tokens: [{id: "XXXXXXXXXXXXXXXXX", value: 1}], offering_tokens: [{id: "XXXXXXXXXXXXXXXXX", value: 1}], second_party_identity_id: $recipientId}) {
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

Use the id: "0" argument for Enjin Coin \(ENJ\).

**Step 2:** Get the trade\_id - param1.

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

**Step 3:** Complete the trade request. Enter param1 as trade\_id, 2nd person identity\_id, and confirm in 2nd person wallet.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation CompleteTradeRequest($id: Int!, $tradeId: String!) { CreateEnjinRequest(identity_id: $id, type: COMPLETE_TRADE, complete_trade_data: {trade_id: $tradeId}) { id transactionId encodedData } }
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## Changing Asset Transfer Status

At times, you may want to change the transfer status of a token you have created to give it a certain value, whether you want the token to be **permanently transferable**, **temporarily transferable**, or **bound** to an address.

**Note**: If you have set the token to be permanently transferable, you will not be able to alter that setting.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation ChangeAssetTransferableType($appId: Int!, $identityId: Int!, $tokenId: String!, $transferable: TokenTransferable!) {
 CreateEnjinRequest(appId: $appId, identityId: $identityId, type: SET_TRANSFERABLE, set_transferable_data: {token_id: $tokenId, transferable: $transferable}) {
   id
   encodedData
 }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```

```
{% endtab %}
{% endtabs %}

## **Blockchain Explorer**

Players are inherently interested in the blockchain data behind the assets they own.

If you would like to link your users to the EnjinX listing of a specific token, you can append the token ID to the end of the URL. This allows them to learn everything they can about their tokens**,** example:

[https://jumpnet.enjinx.io/eth/asset/000000000000000](https://jumpnet.enjinx.io/eth/asset/000000000000000)

[https://enjinx.io/eth/asset/000000000000000](https://enjinx.io/eth/asset/000000000000000)  
****

