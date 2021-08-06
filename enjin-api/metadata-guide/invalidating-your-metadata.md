---
description: Learn how to invalidate the cached asset metadata
---

# Invalidating Your Metadata

If your asset metadata doesn't load or takes a while to load, we have implemented the `Invalidate Metadata` mutation to push the metadata through our servers so that your asset metadata can appear instantly.

```graphql
mutation InvalidateTokenMetadata {
  InvalidateAssetMetadata(id: "<tokenId>")
}
```

`Id` is the token ID of the asset you want to invalidate.

This mutation will instruct the Platform to invalidate the metadata and thus fetch it again, directly from your server.

Please note of the following when running this particular mutation:

1. It can take a few minutes, after invalidating your asset, for the new metadata to load. 
2. This mutation can only be run once, per asset, every few minutes. 
3. You can only run this mutation on assets that belong to a project, in which you have the minter role \(or higher\) on.

