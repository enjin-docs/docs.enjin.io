---
description: Learn more about setting asset metadata to your NFTs and Digital Assets
---

# Metadata Guide

### Setting Your Asset Metadata

You can set your metadata through the “Assets” section in your project on Enjin’s minting panel by clicking the “Edit” button on the token you wish to customize.

#### **Basic Editor**

If you want to set your metadata the fast and cheap way, you can do so using the “Basic Editor”.

![](https://assets-global.website-files.com/5d56cb37dc00727a4f69850c/60bda54e5efa0121e6f3d5a4_1c671d25cdeeff843d65b328d23c2f14.png)

Your token URI will then be customized to point towards Enjin’s servers, where the metadata is stored.

Once a successful request has been made, you will need to accept and sign the transaction in the **REQUESTS** section of your wallet.

You can also upload .GIF and .MP4 files as your asset images!

Requirements when using hosted metadata:

* 5Mb max for GIFs/regular images.
* 15Mb max for MP4 videos.

#### **Advanced Editor**

If you want full control over your metadata, you can choose the URI using the “Advanced Editor”**.**

![](https://assets-global.website-files.com/5d56cb37dc00727a4f69850c/60bda57e6d4e0dffb1d98947_97479a4c226b02c9a61446732cc1ed09.png)

Your token URI will then be customized to point towards the address you have specified and you will be able to customize the JSON file at your leisure. 

Please note the following requirements when it comes to hosting your own metadata:

**1.** The link \(to both metadata and image\) must be publicly accessible to robots

**2.** The uri must be set appropriately to the requested file

**3.** The image must be that of a valid image file \(the image must show\)

**4.** The JSON must conform with the JSON RFC standards, if it does not conform in any ****way then it won't be loaded.

#### **API**

If you want to set your metadata ****programmatically, you can do so using the following API query.

```graphql
mutation SetItemUri($identityId: Int!, $itemUriData: SetItemUriInput!) {
CreateEnjinRequest(identity_id: $identityId, type: SET_ITEM_URI, set_item_uri_data: $itemUriData) {
  id
  encodedData
  state
}
}
```

The ERC-1155 token standard includes optional formatting to allow for ID substitution by clients. If the string {id} exists in any JSON value, it MUST be replaced with the actual token ID, by all client software that follows this standard.

* The string format of the substituted hexadecimal ID MUST be lowercase alphanumeric: \[0-9a-f\] with no 0x prefix.
* The string format of the substituted hexadecimal ID MUST be leading zero-padded to 64 hex characters length if necessary.

In this situation, the following address: _https://token-cdn-domain/{id}.json_

Would be replaced with: _https://token-cdn-domain/780000000000001e000000000000000000000000000000000000000000000000.json_

