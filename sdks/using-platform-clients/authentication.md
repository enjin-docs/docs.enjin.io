# Authentication

### Creating the Client

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.EnjinHosts;
import com.enjin.sdk.ProjectClient;

ProjectClient client = new ProjectClient(EnjinHosts.KOVAN);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK;

ProjectClient client = new ProjectClient(EnjinHosts.KOVAN);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/EnjinHosts.hpp"
#include "enjinsdk/ProjectClient.hpp"

using namespace enjin::sdk;

std::unique_ptr<ProjectClient> client = ProjectClientBuilder()
        .base_uri(KOVAN)
        .build();
```
{% endtab %}
{% endtabs %}

### Creating the Authentication Request

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.project.queries.AuthProject;

AuthProject req = new AuthProject()
        .uuid("<your-project's-uuid>")
        .secret("<your-project's-secret>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.ProjectSchema;

AuthProject req = new AuthProject()
        .Uuid("<your-project's-uuid>")
        .Secret("<your-project's-secret>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/project/AuthProject.hpp"

using namespace enjin::sdk::project;

AuthProject req = AuthProject()
        .set_uuid("<your-project's-uuid>")
        .set_secret("<your-project's-secret>");
```
{% endtab %}
{% endtabs %}

### Sending the Request

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.AccessToken;

GraphQLResponse<AccessToken> res = client.authProject(req);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

GraphqlResponse<AccessToken> res = client.AuthProject(req).Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/AccessToken.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

GraphqlResponse<AccessToken> res = client->auth_project(req).get();
```
{% endtab %}
{% endtabs %}

TODO

{% tabs %}
{% tab title="Java" %}
```java
res.isSuccess();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
res.IsSuccess;
```
{% endtab %}

{% tab title="C++" %}
```cpp
res.is_successful();
```
{% endtab %}
{% endtabs %}

### Getting the Result

TODO

{% tabs %}
{% tab title="Java" %}
```java
AccessToken accessToken = res.getData();

client.auth(accessToken.getToken());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
AccessToken accessToken = res.Result;

client.Auth(accessToken.Token);
```
{% endtab %}

{% tab title="C++" %}
```cpp
AccessToken access_token = res.get_result().value();

client->auth(access_token.get_token().value());
```
{% endtab %}
{% endtabs %}

TODO

{% tabs %}
{% tab title="Java" %}
```java
client.isAuthenticated();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
client.IsAuthenticated;
```
{% endtab %}

{% tab title="C++" %}
```cpp
client->is_authenticated();
```
{% endtab %}
{% endtabs %}

TODO

