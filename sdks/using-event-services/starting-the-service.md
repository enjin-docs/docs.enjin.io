# Setting up a Event Service

### Getting the Platform Data

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Platform;
import com.enjin.sdk.schemas.shared.queries.GetPlatform;

GetPlatform req = new GetPlatform()
    .withNotificationDrivers();

// Any authenticated platform client
GraphQLResponse<Platform> res = client.getPlatform(req);

Platform platform = res.getData();
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;
using Enjin.SDK.Shared;

GetPlatform req = new GetPlatform()
    .WithNotificationDrivers();

// Any authenticated platform client
GraphqlResponse<Platform> res = client.GetPlatform(req).Result;

Platform platform = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Platform.hpp"
#include "enjinsdk/shared/GetPlatform.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;
using namespace enjin::sdk::shared;

GetPlatform req = GetPlatform()
    .set_with_notifications();

// Any authenticated platform client
GraphqlResponse<Platform> res = client->get_platform(req).get();

Platform platform = res.get_result().value();
```
{% endtab %}
{% endtabs %}

### Starting a Service

TODO

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.PusherNotificationService;

PusherNotificationService service = new PusherNotificationService(platform);

service.start(); // Returns a future
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;

PusherEventService service = new PusherEventService(platform);

service.Start(); // Returns a task
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/PusherEventService.hpp"
#include <memory>

std::unique_ptr<PusherEventService> service = PusherEventServiceBuilder()
    .platform(platform)
    .build();

service->start(); // Returns a future
```
{% endtab %}
{% endtabs %}

TODO: Shutdown service and check if connected

### Handling Service Events \(TODO: Change section name\)

TODO

#### Java SDK

TODO

```java
import com.enjin.sdk.events.ConnectionEventListener;

service.start(new ConnectionEventListener() {

    public void onConnect() { /* Your code here */ }

    public void onDisconnect() { /* Your code here */ }

    public void onError(Exception e) { /* Your code here */ }

});
```

#### C\# SDK

TODO

```csharp
service.Connected += (sender, args) => { /* Your code here */ };

service.Disconnected += (sender, args) => { /* Your code here */ };

service.Error += (sender, exception) => { /* Your code here */ };
```

#### C++ SDK

TODO

```cpp
service->set_connected_handler([]() { /* Your code here */ });

service->set_disconnected_handler([]() { /* Your code here */ });

service->set_error_handler([](const std::exception& e)> { /* Your code here */ });
```

