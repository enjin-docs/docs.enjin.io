# Managing Players

### Creating a New Player

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.AccessToken;
import com.enjin.sdk.schemas.project.mutations.CreatePlayer;

CreatePlayer req = new CreatePlayer()
    .id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphQLResponse<AccessToken> res = client.createPlayer(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;
using Enjin.SDK.ProjectSchema;

CreatePlayer req = new CreatePlayer()
    .Id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client.CreatePlayer(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/AccessToken.hpp"
#include "enjinsdk/project/CreatePlayer.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;
using namespace enjin::sdk::project;

CreatePlayer req = CreatePlayer()
    .set_id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client->create_player(req).get();
```
{% endtab %}
{% endtabs %}

### Getting a Existing Player

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Player;
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphQLResponse<Player> res = client.getPlayer(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;
using Enjin.SDK.ProjectSchema;

GetPlayer req = new GetPlayer()
    .Id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client.GetPlayer(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Player.hpp"
#include "enjinsdk/project/GetPlayer.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;
using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<your-player's-id>");

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client->get_player(req).get();
```
{% endtab %}
{% endtabs %}

### Linking a Player

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.LinkingInfo;
import com.enjin.sdk.models.Player;
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<your-player's-id>")
    .withLinkingInfo();

// Using a authenticated ProjectClient
GraphQLResponse<Player> res = client.getPlayer(req);

Player player = res.getData();
LinkingInfo linkingInfo = player.getLinkingInfo();

String code = linkingInfo.getCode();
String qr = linkingInfo.getQr();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;
using Enjin.SDK.ProjectSchema;
using Enjin.SDK.Shared;

GetPlayer req = new GetPlayer()
    .Id("<your-player's-id>")
    .WithLinkingInfo();

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client.GetPlayer(req).Result;

Player player = res.Result;
LinkingInfo linkingInfo = player.LinkingInfo;

string code = linkingInfo.Code;
string qr = linkingInfo.Qr;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/LinkingInfo.hpp"
#include "enjinsdk/models/Player.hpp"
#include "enjinsdk/project/GetPlayer.hpp"
#include <string>

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;
using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<your-player's-id>")
    .set_with_linking_info();

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client->get_player(req).get();

Player player = res.get_result().value();
LinkingInfo linking_info = player.get_linking_info().value();

std::string code = linking_info.get_code().value();
std::string qr = linking_info.get_qr().value();
```
{% endtab %}
{% endtabs %}

TODO: Note that linking info may be null if player already has a wallet linked to them

### Unlinking a Player

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Player;
import com.enjin.sdk.models.Wallet;
import com.enjin.sdk.schemas.project.queries.GetPlayer;

GetPlayer req = new GetPlayer()
    .id("<your-player's-id>")
    .withWallet();

// Using a authenticated ProjectClient
GraphQLResponse<Player> res = client.getPlayer(req);

Player player = res.getData();
Wallet wallet = player.getWallet();

String ethAddress = wallet.getEthAddress();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;
using Enjin.SDK.ProjectSchema;
using Enjin.SDK.Shared;

GetPlayer req = new GetPlayer()
    .Id("<your-player's-id>")
    .WithWallet();

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client.GetPlayer(req).Result;

Player player = res.Result;
Wallet wallet = player.Wallet;

string ethAddress = wallet.EthAddress;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Player.hpp"
#include "enjinsdk/models/Wallet.hpp"
#include "enjinsdk/project/GetPlayer.hpp"
#include <string>

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;
using namespace enjin::sdk::project;

GetPlayer req = GetPlayer()
    .set_id("<your-player's-id>")
    .set_with_wallet();

// Using a authenticated ProjectClient
GraphqlResponse<Player> res = client->get_player(req).get();

Player player = res.get_result().value();
Wallet wallet = player.get_wallet().value();

std::string eth_address = wallet.get_eth_address().value();
```
{% endtab %}
{% endtabs %}

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.schemas.project.mutations.UnlinkWallet;

UnlinkWallet req = new UnlinkWallet()
    .ethAddress("<your-player's-eth-address>");

// Using a authenticated ProjectClient
GraphQLResponse<Boolean> res = client.unlinkWallet(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.ProjectSchema;

UnlinkWallet req = new UnlinkWallet()
    .EthAddress("<your-player's-eth-address>");

// Using a authenticated ProjectClient
GraphqlResponse<bool> res = client.UnlinkWallet(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/project/UnlinkWallet.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::project;

UnlinkWallet req = UnlinkWallet()
    .set_eth_address("<your-player's-eth-address>");

// Using a authenticated ProjectClient
GraphqlResponse<bool> res = client->unlink_wallet(req).get();
```
{% endtab %}
{% endtabs %}

TODO

