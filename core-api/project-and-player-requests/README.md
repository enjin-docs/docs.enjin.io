---
description: Learn more about the Project and Player Schema
---

# Project & Player Requests

The project schema has all of its queries and mutations scoped to a singular project. This means that a project access token has unfettered control over everything to do with itself, this includes player authentication.

The player schema, on the other hand, is restricted to a singular player for a given project. This means that they can only query/mutate data that relates directly to themselves. This means that you cannot, for example, fetch the wallet address of another player or retrieve a list of players for the project.

**A project** can do any task related to itself or its players (eg. the project can query any player's wallet). This is like an admin.

**A player** can only do tasks related to itself (eg. Bob can only query their own wallet, cannot query Alice's wallet) Cannot create assets.

V.2 schemas are available to apply to your project as a beta feature.

{% hint style="info" %}
You can enable v.2 schemas on your project (Mainnet, JumpNet or Kovan) by following this guide [here](https://enjin.io/help/v2-schemas-beta-release).&#x20;
{% endhint %}

To access the latest schemas, select a network you are working with:

* **Mainnet:** [https://cloud.enjin.io/graphql/playground](https://cloud.enjin.io/graphql/playground)
* **Kovan:** [https://kovan.cloud.enjin.io/graphql/playground](https://kovan.cloud.enjin.io/graphql/playground)
* **JumpNet:** [https://jumpnet.cloud.enjin.io/graphql/playground](https://jumpnet.cloud.enjin.io/graphql/playground)

_**Note:** You can now enable v.2 schemas on your project (Mainnet, JumpNet and/or Kovan). To do this, follow this guide_ [_here_](https://enjin.io/help/v2-schemas-beta-release)_._
