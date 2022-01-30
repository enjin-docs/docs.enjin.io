# Managing Assets

{% hint style="info" %}
#### Beta Documentation

The documentation for the Enjin SDKs pertain to the Project and Player schemas which are currently in an **Beta** release. To enable The Project and Player schema, please follow this guide [here](https://enjin.io/help/v2-schemas-beta-release). For any queries, please contact [Enjin Support](mailto:support@enjin.io).
{% endhint %}

## Minting Assets

To mint assets to a wallet we may use the `MintAsset` request. This request is only available for the project schema, therefore we will need an [authenticated](authentication.md#authenticating-a-project-client) project client.

#### Step 1: Create the Mint Data

Before creating the request proper we may prefer to create the `MintInput` data that we will be supplying to the request. For creating the input data we need to specify the wallet address we would like the minted assets to go to as well as the number assets we wish to mint. An example of creating the `MintInput` data can be seen in the code block below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.MintInput;

MintInput input = new MintInput()
    .to("<the-recipient's-address>")
    .value("<the-number-of-assets>");
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Models;

MintInput input = new MintInput()
    .To("<the-recipient's-address>")
    .Value("<the-number-of-assets>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/MintInput.hpp"

using namespace enjin::sdk::models;

MintInput input = MintInput()
    .set_to("<the-recipient's-address>")
    .set_value("<the-number-of-assets>");
```
{% endtab %}
{% endtabs %}

#### Step 2: Create the Request

Once we have created all the inputs we desire we can start taking a look at creating the request itself. For the request we will use the `MintAsset` request. This request requires us to provide the address of a project wallet, the ID of the asset we are minting, and the input data for the mint(s) we are performing as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.MintAsset;

MintAsset req = new MintAsset()
    .ethAddress("<the-wallet's-address>")
    .assetId("<the-asset's-id>")
    .mints(input /* append any additional inputs */));
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.ProjectSchema;

MintAsset req = new MintAsset()
    .EthAddress("<the-wallet's-address>")
    .AssetId("<the-asset's-id>")
    .Mints(input /* append any additional inputs */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/MintAsset.hpp"

using namespace enjin::sdk::project;

MintAsset req = MintAsset()
    .set_eth_address("<the-wallet's-address>")
    .set_asset_id("<the-asset's-id>")
    .set_mints({ input /* append any additional inputs */ });
```
{% endtab %}
{% endtabs %}

#### Step 3: Send the Request

Now that we have created our request we need to send it to the platform using our client's method for minting assets. For this method we expect to receive a GraphQL response wrapping a `Request` model with details for the transaction.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Request;

// Using a authenticated ProjectClient
GraphQLResponse<Request> res = client.mintAsset(req);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated ProjectClient
GraphqlResponse<Request> res = client.MintAsset(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Request.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated ProjectClient
GraphqlResponse<Request> res = client->mint_asset(req).get();
```
{% endtab %}
{% endtabs %}

## Melting Assets

#### Step 1: Create the Melt Data

To melt assets we first start by creating the `Melt` model containing the data for the request. The data we need to set for this model is the asset ID and depending on if the asset being melted is an NFT, then we will need to specify the index and if the asset is not an NFT, then we will specify the amount of the asset being melted instead.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.Melt;

Melt melt = new Melt()
    .assetId("<the-asset's-id>")
    .assetIndex("<the-asset's-index>") // Set this value for NFT's
    .value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Models;

Melt melt = new Melt()
    .AssetId("<the-asset's-id>")
    .AssetIndex("<the-asset's-index>") // Set this value for NFT's
    .Value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/Melt.hpp"

using namespace enjin::sdk::models;

Melt melt = Melt()
    .set_asset_id("<the-asset's-id>")
    .set_asset_index("<the-asset's-index>") // Set this value for NFT's
    .set_value("<the-number-of-assets>");   // Set this value for FT's
```
{% endtab %}
{% endtabs %}

#### Step 2: Create the Request

Next we will create the `MeltAsset` request we will be sending. This request accepts the melt data we created in the previous step as well as any additional melt data we may have created since. However, depending on the schema we are using we may need to provide additional data.

In the project schema we must specify a project wallet that the request is operating on. An example of this is shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.MeltAsset;

MeltAsset req = new MeltAsset()
    .ethAddress("<the-wallet's-address>")
    .melts(melt /* append any additional melts */);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.ProjectSchema;

MeltAsset req = new MeltAsset()
    .EthAddress("<the-wallet's-address>")
    .Melts(melt /* append any additional melts */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/MeltAsset.hpp"

using namespace enjin::sdk::project;

MeltAsset req = MeltAsset()
    .set_eth_address("<the-wallet's-address>")
    .set_melts({melt /* append any additional melts */});
```
{% endtab %}
{% endtabs %}

In the player schema we need not provide any additional data aside from the melt data, as the platform infers the which wallet the request operates on by using our client's credentials.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.mutations.MeltAsset;

MeltAsset req = new MeltAsset()
    .melts(melt /* append any additional melts */);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.PlayerSchema;

MeltAsset req = new MeltAsset()
    .Melts(melt /* append any additional melts */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/MeltAsset.hpp"

using namespace enjin::sdk::player;

MeltAsset req = MeltAsset()
    .set_melts({melt /* append any additional melts */});
```
{% endtab %}
{% endtabs %}

#### Step 3: Send the Request

With our created request we may now send it to the platform using our client's method for melting assets. The response we expect to receive is a GraphQL response wrapping a `Request` model containing details for the transaction.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Request;

// Using a authenticated client
GraphQLResponse<Request> res = client.meltAsset(req);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated client
GraphqlResponse<Request> res = client.MeltAsset(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Request.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated client
GraphqlResponse<Request> res = client->melt_asset(req).get();
```
{% endtab %}
{% endtabs %}

## Sending Assets

### Sending One Asset

#### Step 1: Create the Request

The request we will be using to send a single asset is the `SendAsset` request. To create this request we must now the wallet address of the recipient we are sending the asset to, the ID of the asset, and depending on if the asset is an NFT or not we will need to either know its index if it is an NFT or the amount we wish to send if it is not an not an NFT. In addition to these argument, the schema we are using may necessitate setting special arguments.

When using the project schema to send the request we must specify a project wallet that the transaction will operate on. An example of the created request can be seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.SendAsset;

SendAsset req = new SendAsset()
    .ethAddress("<the-wallet's-address>")
    .recipientAddress("<the-recipient's-address>")
    .assetId("<the-asset's-id>")
    .assetIndex("<the-asset's-index>") // Set this value for NFT's
    .value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.ProjectSchema;

SendAsset req = new SendAsset()
    .EthAddress("<the-wallet's-address>")
    .RecipientAddress("<the-recipient's-address>")
    .AssetId("<the-asset's-id>")
    .AssetIndex("<the-asset's-index>") // Set this value for NFT's
    .Value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/SendAsset.hpp"

using namespace enjin::sdk::project;

SendAsset req = SendAsset()
    .set_eth_address("<the-wallet's-address>")
    .set_recipient_address("<the-recipient's-address>")
    .set_asset_id("<the-asset's-id>")
    .set_asset_index("<the-asset's-index>") // Set this value for NFT's
    .set_value("<the-number-of-assets>");   // Set this value for FT's
```
{% endtab %}
{% endtabs %}

When using the player schema to send the request we do not specify a wallet for the transaction as this is inferred from our player client's credentials.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.mutations.SendAsset;

SendAsset req = new SendAsset()
    .recipientAddress("<the-recipient's-address>")
    .assetId("<the-asset's-id>")
    .assetIndex("<the-asset's-index>") // Set this value for NFT's
    .value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.PlayerSchema;

SendAsset req = new SendAsset()
    .RecipientAddress("<the-recipient's-address>")
    .AssetId("<the-asset's-id>")
    .AssetIndex("<the-asset's-index>") // Set this value for NFT's
    .Value("<the-number-of-assets>");  // Set this value for FT's
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/SendAsset.hpp"

using namespace enjin::sdk::player;

SendAsset req = SendAsset()
    .set_recipient_address("<the-recipient's-address>")
    .set_asset_id("<the-asset's-id>")
    .set_asset_index("<the-asset's-index>") // Set this value for NFT's
    .set_value("<the-number-of-assets>");   // Set this value for FT's
```
{% endtab %}
{% endtabs %}

#### Step 2: Send the Request

With the request created we can now send it to the platform for processing by using the method in our client that has the same name as the request itself. In response we will receive the `Request` model with details for the transaction.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Request;

// Using a authenticated client
GraphQLResponse<Request> res = client.sendAsset(req);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated client
GraphqlResponse<Request> res = client.SendAsset(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Request.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated client
GraphqlResponse<Request> res = client->send_asset(req).get();
```
{% endtab %}
{% endtabs %}

### Sending Multiple Assets

#### Step 1: Create the Transfer Data

To send multiple assets with a request we will need to setup the transfer data which details each send in the batch request. For this data we specify the wallet address the fund is originating from, the wallet address it is heading to, and the asset data such as the ID, the index if it is a NFT or the amount if not.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.Transfers;

Transfers transfers = new Transfers()
    .from("<the-source-address>")
    .to("<the-destination-address>")
    .assetId("<the-asset's-id>")
    .assetIndex("<the-asset's-index>") // Set this value for NFT's
    .value("<the-number-of-assets>");  // Set this value for non-NFT's
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Models;

Transfer transfer = new Transfer()
    .From("<the-source-address>")
    .To("<the-destination-address>")
    .AssetId("<the-asset's-id>")
    .AssetIndex("<the-asset's-index>") // Set this value for NFT's
    .Value("<the-number-of-assets>");  // Set this value for non-NFT's
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/Transfer.hpp"

using namespace enjin::sdk::models;

Transfer transfer = Transfer()
    .set_from("<the-source-address>")
    .set_to("<the-destination-address>")
    .set_asset_id("<the-asset's-id>")
    .set_asset_index("<the-asset's-index>") // Set this value for NFT's
    .set_value("<the-number-of-assets>");   // Set this value for non-NFT's
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the asset ID is omitted, then the transfer data will send **ENJ** instead.
{% endhint %}

#### Step 2: Create the Request

Next we create the `AdvancedSendAsset` request that we will be sending to the platform. For this request we will be using a chaining method to pass the transfer data we created as well as any additional transfers we might add. However, what additional argument(s) we set for our request is determined by the schema we are using.

When using the project schema to send the request we must specify a project wallet that the transaction will operate on. An example of the created request can be seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.AdvancedSendAsset;

AdvancedSendAsset req = new AdvancedSendAsset()
    .ethAddress("<the-wallet's-address>")
    .transfers(transfers /* append any additional transfers */);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.ProjectSchema;

AdvancedSendAsset req = new AdvancedSendAsset()
    .EthAddress("<the-wallet's-address>")
    .Transfers(transfer /* append any additional transfers */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/AdvancedSendAsset.hpp"

using namespace enjin::sdk::project;

AdvancedSendAsset req = AdvancedSendAsset()
    .set_eth_address("<the-wallet's-address>")
    .set_transfers({ transfer /* append any additional transfers */ });
```
{% endtab %}
{% endtabs %}

When using the player schema to send the request we do not specify a wallet for the transaction as this is inferred from our player client's credentials. Therefore we need only pass the transfer(s) data as shown:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.mutations.AdvancedSendAsset;

AdvancedSendAsset req = new AdvancedSendAsset()
    .transfers(transfers /* append any additional transfers */);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.PlayerSchema;

AdvancedSendAsset req = new AdvancedSendAsset()
    .Transfers(transfer /* append any additional transfers */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/AdvancedSendAsset.hpp"

using namespace enjin::sdk::player;

AdvancedSendAsset req = AdvancedSendAsset()
    .set_transfers({ transfer /* append any additional transfers */ });
```
{% endtab %}
{% endtabs %}

#### Step 3: Send the Request

With the request created we can now send it to the platform for processing. In response we will receive the `Request` model with details for the transaction.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Request;

// Using a authenticated client
GraphQLResponse<Request> res = client.advancedSendAsset(req);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated client
GraphqlResponse<Request> res = client.AdvancedSendAsset(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Request.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated client
GraphqlResponse<Request> res = client->advanced_send_asset(req).get();
```
{% endtab %}
{% endtabs %}
