---
description: Learn how to invalidate your asset metadata.
---

# Invalidating Your Metadata

Sometimes for any reason, if your metadata doesn't load or takes a while to load, we have implemented the `Invalidate Metadata` mutation.

```graphql
mutation InvalidateTokenMetadata {
 InvalidateTokenMetadata(id: "$id")
}
```

`Id` is the token ID of the asset.

This mutation will instruct the Platform to invalidate the metadata and thus fetch it again, directly from your server.

Please be aware that it can take a few minutes, after invalidating it, for the new metadata to load.

Additionally, please be aware that this mutation can only be run once, per token, every few minutes.

You can only run this mutation on tokens that belong to an application that you have the minter role \(or higher\) on.

