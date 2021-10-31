---
description: Learn more about bridging your ENJ & ERC-1155 assets using the JumpNet Bridge.
---

# JumpNet Bridges

JumpNet bridges allows you to transfer tokens between Ethereum Mainnet and Enjin JumpNet.

Using the Bridge, both Enjin Coin (ENJ) and ERC-1155 assets created using the Enjin Platform can be moved back and forth between JumpNet and Ethereum.

The Enjin Bridge receives an asset on one network; once claimed, it replicates the asset on the corresponding network.

{% hint style="info" %}
Currently, the asset bridging functionality is only accessible through the Enjin Platform API. The user interface component, accessible within the Enjin Wallet, will be released at a later stage.
{% endhint %}

#### **Mutations:**

The Enjin Bridge has 3 mutations:

| Mutation                                                  | Usage                                         |
| --------------------------------------------------------- | --------------------------------------------- |
| [BridgeAsset](jumpnet-bridges.md#bridgeasset)             | Used to transfer a single asset.              |
| [BridgeAssets](jumpnet-bridges.md#bridgeassets)           | Used to transfer multiple assets.             |
| [BridgeClaimAssets](jumpnet-bridges.md#bridgeclaimassets) | Used to claim assets on the opposite network. |

### BridgeAsset

The `BridgeAsset` mutation allows you to send one single asset/NFT to the bridge contract. You can run the following mutation to get started:

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation BridgeAsset(
  $assetId: String!
  $assetIndex: String
  $value: BigInt = "1"
  $wallet: EthAddress
) {
  BridgeAsset(
    assetId: $assetId
    assetIndex: $assetIndex
    value: $value
    wallet: $wallet
  ) {
    id
  }
}
```
{% endtab %}
{% endtabs %}

**Steps & Process:**

1. Call the `BridgeAsset` mutation.
2. Confirm the request in your wallet.
3. The asset will moved from your address to the bridge, ready to be claimed from the other side of the bridge.

**Arguments:**

* `assetId` (type: `String!`, example: `"7000000000000002"`)
* `assetIndex` (optional, type: `String`, example: `"0"`)
* `value` (optional, type: `BigInt`, example: `"5"`, default: `"1"`)
  * Must be omitted, or `"1"`, when asset is non-fungible.
* `wallet` (optional, type: `EthAddress`, project-schema only)

### BridgeAssets

The `BridgeAssets` mutation allows you to send multiple digital assets/non-fungible tokens (NFTs).

You can send multiple different indexes using the `BridgeAssets` function.

{% hint style="info" %}
The maximum number of indexes that can be bridged at any given time is 100 per transaction.
{% endhint %}

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation BridgeAssets(
  $assetId: String!
  $assetIndexes: [String!]!
  $wallet: EthAddress
) {
  BridgeAssets(
    assetId: $assetId
    assetIndexes: $assetIndexes
    wallet: $wallet
  ) {
    id
  }
}
```
{% endtab %}
{% endtabs %}

**Steps & Process:**

1. Call the `BridgeAssets` mutation.
2. Confirm the request in the wallet.
3. The assets will be moved from your address to the bridge, ready to be claimed from the other side of the bridge.

**Arguments:**

* `assetId` (type: `String!`, example: `"7000000000000002"`)
* `assetIndexes` (optional, type: `[String!]!`, example: `[1, 2, 3]`)
* `wallet` (optional, type: `EthAddress`, project-schema only)

### BridgeClaimAssets

The `BridgeClaimAssets` mutation allows you to claim your asset/NFT on the Enjin Bridge.

{% hint style="warning" %}
This is a **temporary mutation** that will be natively integrated with the upcoming Enjin Wallet 2.0 release. This mutation will therefore be deprecated in the future after support has been implemented into the updated wallet.
{% endhint %}

{% hint style="info" %}
If the asset has never been transferred to the destination network before, this mutation will have to be run twice. The first instance will create the relevant asset definition on the network and after the transaction has been mined you can call this mutation a second time to complete the transfer of the asset to the network.
{% endhint %}

{% tabs %}
{% tab title="GraphQL" %}
```graphql
mutation BridgeClaimAsset($assetId: String!, $wallet: EthAddress) {
  BridgeClaimAsset(assetId: $assetId, wallet: $wallet) {
    id
  }
}
```
{% endtab %}
{% endtabs %}

**Steps & Process:**

1. After the bridging transaction has been mined successfully, wait for approximately 20 blocks. You'll then be able to use this method to claim it on the destination network.
2. You will need to specify the `assetId`, and you can optionally (on the project schema) override the `wallet` in question.
3. Confirm the request in your wallet.
4. The bridge will fulfill the claim by sending you the exact asset initiated from the other side of the bridge.

**Arguments:**

* `assetId` (type: `String!`, example: `"7000000000000002"`)
* `wallet` (optional, type: `EthAddress`, project-schema only)

For any additional assistance, please reach out to [our support team](https://enjin.io/support).
