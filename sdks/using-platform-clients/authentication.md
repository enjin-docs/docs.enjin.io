# Authentication

{% hint style="info" %}
## Alpha Documentation

The documentation for the Enjin SDKs pertain to the Project and Player schemas which are currently in an **Alpha** release. The Project and Player schemas are **not yet publicly available** and therefore this documentation is limited only to those who already have access. For any queries, please contact [Enjin Support](mailto:support@enjin.io).
{% endhint %}

## Authenticating a Project Client

### Creating the Client

The first step we take in setting up our `ProjectClient` is to instantiate it. During this we must specify which network we are using. Our choices are Mainnet, JumpNet, and Kovan. URLs for these networks can be programmatically acquired from the `EnjinHosts` class and passed to the clients. The chosen network must match the one we created our project on.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.EnjinHosts;
import com.enjin.sdk.ProjectClient;

String mainnet = EnjinHosts.MAIN_NET;
String jumpnet = EnjinHosts.JUMP_NET;
String kovan = EnjinHosts.KOVAN;

ProjectClient client = new ProjectClient(/* Enjin host here */);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK;

System.Uri mainnet = EnjinHosts.MAIN_NET;
System.Uri jumpnet = EnjinHosts.JUMP_NET;
System.Uri kovan = EnjinHosts.KOVAN;

ProjectClient client = new ProjectClient(/* Enjin host here */);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/EnjinHosts.hpp"
#include "enjinsdk/ProjectClient.hpp"
#include <memory>
#include <string>

using namespace enjin::sdk;

std::string mainnet = MAIN_NET;
std::string jumpnet = JUMP_NET;
std::string kovan = KOVAN;

std::unique_ptr<ProjectClient> client = ProjectClientBuilder()
        .base_uri(/* Enjin host here */)
        .build();
```
{% endtab %}
{% endtabs %}

### Creating the Authentication Request

Before creating the `AuthProject` request, we must first gather our project's UUID and secret key. To do so, we may navigate to our project page on the Enjin platform and find these items under `Settings`  -&gt;`API Credentials`.

Once the UUID and secret have been acquired, we can pass them to the `AuthProject` request we have created.

{% hint style="danger" %}
You should make sure that you're only authenticating as a project in a **secure environment**. The project's secret enables a **large degree of access** over the project and is intended solely to be ran in an environment managed by the developer. It mustn't be exposed to others.
{% endhint %}

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.AuthProject;

AuthProject req = new AuthProject()
        .uuid("<the-project's-uuid>")
        .secret("<the-project's-secret>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

AuthProject req = new AuthProject()
        .Uuid("<the-project's-uuid>")
        .Secret("<the-project's-secret>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/AuthProject.hpp"

using namespace enjin::sdk::project;

AuthProject req = AuthProject()
        .set_uuid("<the-project's-uuid>")
        .set_secret("<the-project's-secret>");
```
{% endtab %}
{% endtabs %}

### Sending the Authentication Request

To send any request to the platform, we must call the method in our client whose name matches the request. The result of these methods in a synchronous operation will be a GraphQL response that wraps the data we want. An example of what this looks like for the `AuthProject` request is shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;

GraphQLResponse<AccessToken> res = client.authProject(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;

GraphqlResponse<AccessToken> res = client.AuthProject(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"

using namespace enjin::sdk::graphql;

GraphqlResponse<AccessToken> res = client->auth_project(req).get();
```
{% endtab %}
{% endtabs %}

With the GraphQL response from the platform we can get the data contained within it. For authentication requests this will be a `AccessToken` class representing the platform's `Auth` type. Before retrieving the data however, we may want to consider checking if the response was successful. To do so, we can use the method shown below and get its result:

{% tabs %}
{% tab title="Java" %}
```java
boolean result = res.isSuccess();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
bool result = res.IsSuccess;
```
{% endtab %}

{% tab title="C++" %}
```cpp
bool result = res.is_successful();
```
{% endtab %}
{% endtabs %}

Now that we have determined that the response was successful we can retrieve the `AccessToken` model from the response. This may be done with the code shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.AccessToken;

AccessToken accessToken = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Models;

AccessToken accessToken = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/AccessToken.hpp"

using namespace enjin::sdk::models;

AccessToken access_token = res.get_result().value();
```
{% endtab %}
{% endtabs %}

### Authenticating

With the `AccessToken` we can now pass the string token contained within to the client's authentication method.

{% tabs %}
{% tab title="Java" %}
```java
client.auth(accessToken.getToken());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
client.Auth(accessToken.Token);
```
{% endtab %}

{% tab title="C++" %}
```cpp
client->auth(access_token.get_token().value());
```
{% endtab %}
{% endtabs %}

After authenticating, we may check to see if the authentication was successful. We can do so with the method shown below and getting the Boolean value returned.

{% tabs %}
{% tab title="Java" %}
```java
boolean result = client.isAuthenticated();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
bool result = client.IsAuthenticated;
```
{% endtab %}

{% tab title="C++" %}
```cpp
bool result = client->is_authenticated();
```
{% endtab %}
{% endtabs %}

With our client successfully authenticated we can now use it to make further requests to the platform. One point of note though is that our client's authentication with the platform will eventual expire. The time in seconds until the authentication expires can retrieved from the `AccessToken` as shown below:

{% tabs %}
{% tab title="Java" %}
```java
long time = accessToken.getExpiresIn();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
long time = accessToken.ExpiresIn.Value;
```
{% endtab %}

{% tab title="C++" %}
```cpp
long time = access_token.get_expires_in().value();
```
{% endtab %}
{% endtabs %}

## Authenticating a Player Client

To authenticate a player client we must first instantiate and authenticate a project client, which has access to the schemas we need. Read over the [Authenticate a Project Client](authentication.md#authenticating-a-project-client) section for steps on setting up a project client ready to send requests to the platform.

### Getting the Access Token

Currently there are two ways to get the access token for authenticating a player client. One such way is through the `CreatePlayer` request, which is for new players that do not yet exist for our project. The other way to acquire a player's access token is via the `AuthPlayer` request, which is used for existing players.

#### Creating a New Player

When using the `CreatePlayer` request, we provide the ID of the new player we wish to add to our project as shown below:

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

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client.CreatePlayer(req).Result;
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

With the request in hand, we can now send the `CreatePlayer` request to the platform and if successful we will get the player's access token in the response as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.AccessToken;

// Using a authenticated ProjectClient
GraphQLResponse<AccessToken> res = client.createPlayer(req);

AccessToken accessToken = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client.CreatePlayer(req).Result;

AccessToken accessToken = res.Result;
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

AccessToken access_token = res.get_result().value();
```
{% endtab %}
{% endtabs %}

#### Authenticating an Existing Player

When using the `AuthPlayer` request, we must specify the ID of the player whom we wish to authenticate for as shown below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.AuthPlayer;

AuthPlayer req = new AuthPlayer()
    .id("<the-player's-id>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

AuthPlayer req = new AuthPlayer()
    .Id("<the-player's-id>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/AuthPlayer.hpp"

using namespace enjin::sdk::project;

AuthPlayer req = AuthPlayer()
    .set_id("<the-player's-id>");
```
{% endtab %}
{% endtabs %}

With the request in hand, we can now send the `AuthPlayer` request to the platform and get the player's access token.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.AccessToken;

// Using a authenticated ProjectClient
GraphQLResponse<AccessToken> res = client.authPlayer(req);

AccessToken accessToken = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client.AuthPlayer(req).Result;

AccessToken accessToken = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/AccessToken.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Using a authenticated ProjectClient
GraphqlResponse<AccessToken> res = client->auth_player(req).get();

AccessToken access_token = res.get_result().value();
```
{% endtab %}
{% endtabs %}

### Authenticating the Client

#### Step 1: Create the Client

Creating a player client is similar to creating a project client, but instead of using the `ProjectClient` and its related classes we will be using the `PlayerClient` class.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.PlayerClient;

PlayerClient playerClient = new PlayerClient("<enjin-host-url>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK;

PlayerClient playerClient = new PlayerClient("<enjin-host-url>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/PlayerClient.hpp"
#include <memory>

using namespace enjin::sdk;

std::unique_ptr<PlayerClient> player_client = PlayerClientBuilder()
            .base_uri("<enjin-host-url>")
            .build();
```
{% endtab %}
{% endtabs %}

#### Step 2: Pass the String Token

Once the player client has been created, it may be authenticated with the access token we received from the platform using either the `CreatePlayer` or `AuthPlayer` requests. To do so, we call the respective authentication method and provide the string token contained within.

{% tabs %}
{% tab title="Java" %}
```java
playerClient.auth(accessToken.getToken());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
playerClient.Auth(accessToken.Token);
```
{% endtab %}

{% tab title="C++" %}
```cpp
player_client->auth(access_token.get_token().value());
```
{% endtab %}
{% endtabs %}

As with the project client, we may check if the token was valid by using the method seen below and getting its Boolean value.

{% tabs %}
{% tab title="Java" %}
```java
boolean result = playerClient.isAuthenticated();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
bool result = playerClient.IsAuthenticated;
```
{% endtab %}

{% tab title="C++" %}
```cpp
bool result = player_client->is_authenticated();
```
{% endtab %}
{% endtabs %}

