# Managing Players

## Important Notice - Alpha Documentation

The documentation for the Enjin SDKs pertain to the Project and Player schemas which are currently in an **Alpha** release. The Project and Player schemas are **not yet publicly available** and therefore this documentation is limited only to those who already have access. For any queries, please contact [Enjin Support](mailto:support@enjin.io).

## Creating a New Player

The first step in player management is to create a player for our project. By creating a player for our project we will be able to link their Enjin Wallet to the project enabling us to create interactions for melting, sending, and trading assets within our application for users.

#### Step 1: Create the Request

To create a player we will be using the `CreatePlayer` request. For this request we will need to set the ID we want for our player as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.CreatePlayer;

CreatePlayer req = new CreatePlayer()
    .id("<the-player's-id>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

CreatePlayer req = new CreatePlayer()
    .Id("<the-player's-id>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/CreatePlayer.hpp"

using namespace enjin::sdk::project;

CreatePlayer req = CreatePlayer()
    .set_id("<the-player's-id>");
```
{% endtab %}
{% endtabs %}

#### Step 2: Send the Request

With the `CreatePlayer` request we have created and our `ProjectClient` we can now send the request to the platform as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.AccessToken;

// Using a authenticated ProjectClient
GraphQLResponse<AccessToken> res = client.createPlayer(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client.CreatePlayer(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/AccessToken.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client->create_player(req).get();
```
{% endtab %}
{% endtabs %}

If the request was successful then we will receive the `AccessToken` for the player in the response. With the `AccessToken` we may also now [authenticate](authentication.md#authenticating-a-player-client) a platform client for our new player if we choose to do so.

## Getting an Existing Player

Once there are players created for our project we may want to get the data associated with them. We will go over how may request this data for an individual player in this section.

#### Step 1: Create the Request

When requesting player data, how we create our request depends on the schema we are using.

To create the `GetPlayer` request in the project schema we need to specify the ID of the player whose data we are requesting. For this we use a chaining method for setting the ID as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<the-player's-id>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

GetPlayer req = new GetPlayer()
    .Id("<the-player's-id>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/GetPlayer.hpp"

using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<the-player's-id>");
```
{% endtab %}
{% endtabs %}

When creating the `GetPlayer` in the player schema we do not specify the player's ID, since the platform infers this from our player client's credentials. This means we need only to instantiate the request as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.queries.GetPlayer;

GetPlayer req = new GetPlayer();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.PlayerSchema;

GetPlayer req = new GetPlayer();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/GetPlayer.hpp"

using namespace enjin::sdk::player;

GetPlayer req = GetPlayer();
```
{% endtab %}
{% endtabs %}

#### Step 2: Send the Request

After we have created our request we send it to the platform using our client's corresponding get player method. In the platform's response we expect a `Player` model representing the data we requested, which we may retrieve if the request was successful.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Player;

// Using a authenticated client
GraphQLResponse<Player> res = client.getPlayer(req);

Player player = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated client
GraphqlResponse<Player> res = client.GetPlayer(req).Result;

Player player = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Player.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated client
GraphqlResponse<Player> res = client->get_player(req).get();

Player player = res.get_result().value();
```
{% endtab %}
{% endtabs %}

## Linking a Player

### Linking Information

In the `Player` model there exists a `LinkingInfo` field that contains information we may use to allow our users to link their Enjin Wallet to their player account in our project. When we get a populated `LinkingInfo` model from the platform it will have two fields we are interested in, the code field which contains the linking code users may enter in their Enjin Wallet to link to the project and the QR field which contains the URL to the QR image we can display and have our users scan in place of using the linking code.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.LinkingInfo;

LinkingInfo linkingInfo = /* linking info source */;

String code = linkingInfo.getCode();
String qr = linkingInfo.getQr();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Models;

LinkingInfo linkingInfo = /* linking info source */;

string code = linkingInfo.Code;
string qr = linkingInfo.Qr;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/LinkingInfo.hpp"
#include <string>

using namespace enjin::sdk::models;

LinkingInfo linking_info = /* linking info source */;

std::string code = linking_info.get_code().value();
std::string qr = linking_info.get_qr().value();
```
{% endtab %}
{% endtabs %}

### Getting the Linking Information

There is a minor variation between the project and player schemas when creating the request for getting the player information. For this reason we will cover the creation of the request separately for each client.

#### Creating the Request for a Project Client

We may get the player's linking information using the `GetPlayer` request from the project schema and specify that we want the player data to be returned **with** the player's linking information set. To do so we use two chaining methods. One to set the player's ID and another to set the request to retrieve the linking information as seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<the-player's-id>")
    .withLinkingInfo();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;
using Enjin.SDK.Shared;

GetPlayer req = new GetPlayer()
    .Id("<the-player's-id>")
    .WithLinkingInfo();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/GetPlayer.hpp"

using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<the-player's-id>")
    .set_with_linking_info();
```
{% endtab %}
{% endtabs %}

#### Creating the Request for a Player Client

In the player schema we use the `GetPlayer` request, however unlike in the project schema this `GetPlayer` request does not need the player's ID set, since the platform infers it from our player client's credentials. This means we only need to specify that we want to request the player data **with** the linking information set for our request as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .withLinkingInfo();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.PlayerSchema;
using Enjin.SDK.Shared;

GetPlayer req = new GetPlayer()
    .WithLinkingInfo();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/GetPlayer.hpp"

using namespace enjin::sdk::player;

GetPlayer req = GetPlayer()
    .set_with_linking_info();
```
{% endtab %}
{% endtabs %}

#### Sending the Request

After creating our request we now send it to the platform by using the method in our client of the same name as our request. Once we have the response when can retrieve the data from it.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.LinkingInfo;
import com.enjin.sdk.models.Player;

// Using a authenticated client
GraphQLResponse<Player> res = client.getPlayer(req);

Player player = res.getData();

LinkingInfo linkingInfo = player.getLinkingInfo();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated client
GraphqlResponse<Player> res = client.GetPlayer(req).Result;

Player player = res.Result;

LinkingInfo linkingInfo = player.LinkingInfo;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/LinkingInfo.hpp"
#include "enjinsdk/models/Player.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated client
GraphqlResponse<Player> res = client->get_player(req).get();

Player player = res.get_result().value();

LinkingInfo linking_info = player.get_linking_info().value();
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In the event that the player is already linked to a wallet the `Player` model returned by the platform may **not** have its `LinkingInfo` set.
{% endhint %}

## Unlinking a Player

### Using the Project Client

#### Step 1: Get the Wallet Address

Before creating our request to unlink a player's wallet we must first know what their wallet's address is. If we do not already have this value cached in our application we need not worry as we may retrieve it from the platform with the `GetPlayer` request.

To use the `GetPlayer` request to get the wallet address we must specify that we want the player data to be returned **with** the player's wallet data set. For this we use a chaining method for including wallet data on the request as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<the-player's-id>")
    .withWallet();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;
using Enjin.SDK.Shared;

GetPlayer req = new GetPlayer()
    .Id("<the-player's-id>")
    .WithWallet();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/GetPlayer.hpp"

using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<the-player's-id>")
    .set_with_wallet();
```
{% endtab %}
{% endtabs %}

After creating the request we can now send it to the platform and get the player data returned in the response.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Player;

// Using a authenticated ProjectClient
GraphQLResponse<Player> res = client.getPlayer(req);

Player player = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client.GetPlayer(req).Result;

Player player = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Player.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client->get_player(req).get();

Player player = res.get_result().value();
```
{% endtab %}
{% endtabs %}

The `Player` model contains a `Wallet` model as one of its fields. We can get this field and in turn get the Ethereum address of the wallet.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.Wallet;

Wallet wallet = player.getWallet();

String ethAddress = wallet.getEthAddress();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Models;

Wallet wallet = player.Wallet;

string ethAddress = wallet.EthAddress;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/Wallet.hpp"
#include <string>

using namespace enjin::sdk::models;

Wallet wallet = player.get_wallet().value();

std::string eth_address = wallet.get_eth_address().value();
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
If the player does not have a wallet linked to them then the `Wallet` field will **not** be set.
{% endhint %}

#### Step 2: Create the Request

Once we know the player's wallet address we can create the `UnlinkWallet` request and pass it the wallet address as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.mutations.UnlinkWallet;

UnlinkWallet req = new UnlinkWallet()
    .ethAddress("<the-player's-eth-address>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

UnlinkWallet req = new UnlinkWallet()
    .EthAddress("<the-player's-eth-address>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/UnlinkWallet.hpp"

using namespace enjin::sdk::project;

UnlinkWallet req = UnlinkWallet()
    .set_eth_address("<the-player's-eth-address>");
```
{% endtab %}
{% endtabs %}

#### Step 3: Send the Request

With the created request we now pass it to the client's method with the same name as our request. For `UnlinkWallet` request we expect the returned response to wrap a Boolean value.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;

// Using a authenticated ProjectClient
GraphQLResponse<Boolean> res = client.unlinkWallet(req);

Boolean result = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;

// Using a authenticated ProjectClient
GraphqlResponse<bool> res = client.UnlinkWallet(req).Result;

bool result = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"

using namespace enjin::sdk::graphql;

// Using a authenticated ProjectClient
GraphqlResponse<bool> res = client->unlink_wallet(req).get();

bool result = res.get_result().value();
```
{% endtab %}
{% endtabs %}

The Boolean value contained within the response indicates if the unlink operation was successful. A value of `true` tells us that we successful unlinked our player, whereas a value of `false` may imply that the wallet was already unlinked when we sent our request.

### Using the Player Client

#### Step 1: Create the Request

Unlike with the project schema when we use the `UnlinkWallet` request from the player schema the platform determines the player we intend to unlink using the credentials of our `PlayerClient`. This means that we do not specify our player's wallet address and instead create the `UnlinkWallet` request with no additional setup as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.player.mutations.UnlinkWallet;

UnlinkWallet req = new UnlinkWallet();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.PlayerSchema;

UnlinkWallet req = new UnlinkWallet();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/player/UnlinkWallet.hpp"

using namespace enjin::sdk::player;

UnlinkWallet req = UnlinkWallet();
```
{% endtab %}
{% endtabs %}

#### Step 2: Send the Request

We now pass our request to the client using the method of the same name. Our expected response will wrap a Boolean value which we may retrieve.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;

// Using a authenticated PlayerClient
GraphQLResponse<Boolean> res = client.unlinkWallet(req);

Boolean result = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;

// Using a authenticated PlayerClient
GraphqlResponse<bool> res = client.UnlinkWallet(req).Result;

bool result = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"

using namespace enjin::sdk::graphql;

GraphqlResponse<bool> res = client->unlink_wallet(req).get();

bool result = res.get_result().value();
```
{% endtab %}
{% endtabs %}

The Boolean value contained within the response indicates if the unlink operation was successful. A value of `true` tells us that we successful unlinked our player, whereas a value of `false` may imply that the our player was not linked when we sent our request.

