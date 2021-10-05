# Asset properties

Tokens, also known as blockchain assets, are used to represent the identity of your virtual items on the blockchain.

### Fungible Tokens \(FT\):

Traditional currencies and cryptocurrencies are fungible; they are identical, interchangeable, and divisible. For currencies to work as a standard payment method, fungibility is essential.

Fungible tokens do not have a unique serial number or history; there is nothing to distinguish one from the next. For example, every $5 note is exactly the same and holds the same value. Every half of one fungible token is equal to two-quarters of another.

Fungible tokens are useful for things like currency, reward points, discounts, and promotional materials—any item that doesn't require a unique identity.

### Non-Fungible Tokens \(NFT\):

A non-fungible token is an unique asset.

Non-fungible tokens are not divisible and are stored in the Enjin Wallet as separate tokens with individual data. However, non-fungible tokens are not always 100% unique. For example, a set of tokens may share the same name, description, and image, but they can still be non-fungible if they possess unique, distinguishing properties \(identity, history, and metadata\).

Non-fungible tokens are suitable for things like identification, certificates, collectibles, gaming characters—any asset that requires its own unique identity.

There are two types of data that can be attached to each token.

* **Blockchain Data** is committed permanently to the blockchain. The defining properties of a token, including its identity, settings, and ENJ-backed value can impact the demand for a token drastically. Therefore, much of this data can never be changed once committed to the blockchain. While some token settings can be updated by replacing old data with new data, the previous token settings will remain on record, viewable in the transaction history on the blockchain.
* **Metadata** is the human-readable information that your users will be able to see in your game or app and any other platform where they can see your token. This data can be updated at any time.

### Blockchain Data: Changeable

This data can be edited and replaced with new settings at any time.

**Name:** The name that will be committed to the blockchain.

**Metadata URI:** See [Metadata guide](../metadata-guide/).  
The metadata URI allows you to add a URL that contains a JSON that describes properties of your item, including images.

**Transferable**  
Determines if items are able to be traded, or are bound to their owners \(i.e. non-tradable\).

* **Permanent**: Item is always able to be traded with others. This setting is not changeable once committed to a token.
* **Bound**: Item is always bound to the owner of the item.
* **Temporary**: Item is currently tradable, but the creator can make it non-tradable at a future date.

**transferFeeSettings: value**

If using ENJ, multiply the value by 10^18 to include 18 decimals. When you first set a transfer fee, that setting becomes the maximum fee you can charge. However, you can lower a transfer fee at any time, at which point, you can then raise it back to the amount you initially set.

### Blockchain Data: Permanent

**totalSupply**: This is how many of the item you want to exist. This limit can be broken or mean different things depending on the supply model you use above. For example, if you use the COLLAPSING supply type, the initial supply would represent the total number of items that existed during the original run. The easiest to understand is FIXED, which tells users that there can only be "this many" items of this kind in existence at any one time.

**initialReserve**: This is how many items you want to pre-pay to mint as part of the initial create operation. Minting items will be deducted from this balance until it is exhausted. You have to pay for at least one item on creation. Having an initial reserve allows you to create your item without having to spend all the ENJ for your total supply upon creation.

**transferFeeSettings: type**

You can choose to charge a transfer fee for every peer-to-peer transaction that your users make. This allows you to monetize the economy that surrounds your game and gain revenue by fostering interesting new social dynamics within your community.

* **None**: No Transfer fees are charged when this item changes hands.
* **Per\_Crypto\_Item**: This refers to transfer fee per asset in ENJ, which is cumulative based on the number of assets that is being sent. For example, if an Apple has a 0.1 ENJ transfer fee per item and the user Simon sends 10 apples to user1, then Simon would be charged 1 ENJ for the transaction that would go to the creator of the apple asset.
* **Per\_Transfer**: This refers to transfer fee, per transfer, in ENJ. For example, if an Apple has 0.1 ENJ fee per transfer and Simon sends 10 apples to user1, Simon would be charged 0.1 ENJ for the transaction that would go to the creator of the apple asset.
* **Ratio\_Cut**: Note, to use ratio\_cut, only fungible assets are allowed. A % cut of the total items is subtracted from the total for the creator, with the sender paying the total price. For example, if transferring 500 apples with a 10% ratio cut \(0.1\) the recipient would get 450 apples and the creator, would receive 50 apples, with the sender paying 500 total for the transaction.
* **Ratio\_Extra**: Note, to use ratio\_extra, only fungible assets are allowed. A tax that is charged ON TOP of everything. For example, if transferring 500 apples with a 10% ratio extra, the user would get 500 apples and the creator would receive 50 apples, and the sender pays 550 apples total for the transaction.

**transferFeeSettings:**  
The token ID of the token you want to use as the transfer fee. Use 0 if you want your users to pay you in Enjin Coin.

**meltValue**  
The amount of ENJ you want to use per unit of the item you are creating. You need to use a minimal amount of ENJ to back your items depending on how many you are creating in your initial reserve \(the min-cost will be listed beside the label\). In general, the more items of one type you are making, the less ENJ you need **per unit** of item.

Every token minted needs to be backed by aminimum amount of ENJ that can be calculated using this formula: 0.5 \* Math.sqrt\(initialReserve\) / initialReserve

**supplyModel**: This is how the item pool behaves with respect to minting and melting.

The following are our current supply types:

* **Fixed**: You can have up to TOTAL SUPPLY number of items in circulation at one time.
* **Settable**: Allows you to edit the total supply at any time.
* **Infinite**: You can mint as many items as you want, exceeding TOTAL SUPPLY.
* **Collapsing**: Once melted the items cannot be re-minted.

**meltFeeRatio**  
This is the current percentage of ENJ that the player will receive upon melting the item. The remaining ENJ goes to the creator.

**nonFungible**  
Whether the item is Non-Fungible or Fungible, Boolean value.

### Creating your Asset Metadata

Once you have defined your token's blockchain data by creating the token template, you can add Metadata to it, which is stored in a .json file, hosted somewhere that has public read access.

Please note the following requirements when it comes to metadata:

1. The link \(to both metadata and image\) must be publicly accessible to robots.
2. The uri must be set appropriately to the requested file.
3. The image must be that of a valid image file \(the image must show\).
4. The JSON must conform with the JSON RFC standards, if it does not conform in anyway then it won't be loaded.

Technically, item metadata is optional. Albeit, if you want to display an image and custom item properties in your game, it can result in your asset being extra unique. The Enjin Wallet, and other Enjin Services will also display your assets, based on the metadata that you set.

You can include a name \(which would be displayed instead of the blockchain item name\), description, and link to an image, such as the following example:

```text
{
 "name": "item_name",
 "description": "Description line 1.\nDescription line 2.",
 "image": "/image.jpg"
}
```

You will need to save that file, as a .json file. Once you have that .json file uploaded with public read access, you can make the request to set the item URI \(Uniform Resource Identifier\).

See [this guide](../metadata-guide/) for more details if you are unfamiliar with hosting files.

The following mutation will set Item URI on your asset:

```graphql
mutation SetItemUri($identityId: Int!, $itemUriData: SetItemUriInput!) {
 CreateEnjinRequest(identity_id: $identityId, type: SET_ITEM_URI, set_item_uri_data: $itemUriData) {
   id
   encodedData
   state
 }
}
```

**Advanced Users:** The URI value allows for ID substitution by clients. If the string {id} exists in any URI, clients must replace this with the actual token ID in hexadecimal form. This allows for large number of tokens to use the same on-chain string by defining a URI once, for a large collection of tokens.

Example of such a URI: `https://token-cdn-domain/{id}.json would be replaced with https://token-cdn-domain/780000000000001e000000000000000000000000000000000000000000000000.json`if the client is referring to token ID `780000000000001e000000000000000000000000000000000000000000000000.`

See [Metadata](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1155.md#metadata) section in the ERC-1155 standards documentation for full details.

Once a successful request has been made, you will need to accept and sign the transaction in the **REQUESTS** section of your wallet.

