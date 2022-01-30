# Setting up a Event Service

{% hint style="info" %}
#### Beta Documentation

The documentation for the Enjin SDKs pertain to the Project and Player schemas which are currently in an **Beta** release. To enable The Project and Player schema, please follow this guide [here](https://enjin.io/help/v2-schemas-beta-release). For any queries, please contact [Enjin Support](mailto:support@enjin.io).
{% endhint %}

## Setup & Start

#### Step 1: Getting the Platform Data

Before starting the Pusher event service we first need to request information from the platform related to its notification settings. For the Pusher service, this will be the cluster our service needs to connect to, the key it needs to connect, as well as any other options the platform has specified.

To get the platform information we use the `GetPlatform` request that is shared between and usable by both the `ProjectClient` and the `PlayerClient`, allowing us to use either one for this step. When creating the request we need to specify that we want our response **with** the platform's notification settings. This can be done so with a chaining method as shown in the example below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.schemas.shared.queries.GetPlatform;

GetPlatform req = new GetPlatform()
    .withNotificationDrivers();
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Shared;

GetPlatform req = new GetPlatform()
    .WithNotificationDrivers();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/shared/GetPlatform.hpp"

using namespace enjin::sdk::shared;

GetPlatform req = GetPlatform()
    .set_with_notifications();
```
{% endtab %}
{% endtabs %}

Now that we have created the request we can send it to the platform. We will need to use the method with the matching name as our request and the result we are expecting is a GraphQL response wrapping the `Platform` model, which represents the type of the same name in the platform's API.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.models.Platform;

// Any authenticated client
GraphQLResponse<Platform> res = client.getPlatform(req);

Platform platform = res.getData();
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Graphql;
using Enjin.SDK.Models;

// Any authenticated client
GraphqlResponse<Platform> res = client.GetPlatform(req).Result;

Platform platform = res.Result;
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/GraphqlResponse.hpp"
#include "enjinsdk/models/Platform.hpp"

using namespace enjin::sdk::graphql;
using namespace enjin::sdk::models;

// Any authenticated client
GraphqlResponse<Platform> res = client->get_platform(req).get();

Platform platform = res.get_result().value();
```
{% endtab %}
{% endtabs %}

#### Step 2: Starting the Service

To start the Pusher event service we construct it and pass the `Platform` model instance from the previous step into its constructor.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.PusherNotificationService;

PusherNotificationService service = new PusherNotificationService(platform);
```
{% endtab %}

{% tab title="C#" %}
```csharp
using Enjin.SDK.Events;

PusherEventService service = new PusherEventService(platform);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/PusherEventService.hpp"
#include <memory>

std::unique_ptr<PusherEventService> service = PusherEventServiceBuilder()
    .platform(platform)
    .build();
```
{% endtab %}
{% endtabs %}

Now that we have instantiated our event service we may call its start method. Starting the service tends to involve asynchronous processes. For this reason, event services in the SDKs return an asynchronous type, which we may use to wait for the process to complete if we choose to do so.

{% tabs %}
{% tab title="Java" %}
```java
import java.util.concurrent.Future;

Future<Void> future = service.start();
```
{% endtab %}

{% tab title="C#" %}
```csharp
using System.Threading.Tasks;

Task task = service.Start();
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include <future>

std::future<void> future = service->start();
```
{% endtab %}
{% endtabs %}

Additionally the event service comes with a method which we may use at any time to check if the event service is connected to the server as shown below:

{% tabs %}
{% tab title="Java" %}
```java
boolean result = service.isConnected();
```
{% endtab %}

{% tab title="C#" %}
```csharp
bool result = service.IsConnected();
```
{% endtab %}

{% tab title="C++" %}
```cpp
bool result = service->is_connected();
```
{% endtab %}
{% endtabs %}

#### Step 3: Shutting Down the Service

Once we are done using the event service we may want to shut it down to free up any resources that may have been acquired during its lifetime. To do so we call the service's shutdown method, and as with the start method, we may use the asynchronous type returned to wait for this process to finish.

{% tabs %}
{% tab title="Java" %}
```java
Future<Void> future = service.shutdown();
```
{% endtab %}

{% tab title="C#" %}
```csharp
Task task = service.Shutdown();
```
{% endtab %}

{% tab title="C++" %}
```cpp
std::future<void> future = service->shutdown();
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
In the C++ SDK the destructor for the `PusherEventService` runs the `shutdown()` member-function as well.
{% endhint %}

## Service Notifications

The event services offer ways for us to listen for and handle when certain flags are raised within them, such as when they establish a connection with the server, are disconnected from the server, or encounter an error. However, the API for doing so varies between the SDKs, so we will look at them individually throughout this section.

### Java SDK

For the Java SDK we provide the `ConnectionEventListener` interface which may be passed to the service through any of the `start()` methods which accept it as an argument. The example code block below shows how this listener may be set with an anonymous class.

```java
import com.enjin.sdk.events.ConnectionEventListener;

service.start(new ConnectionEventListener() {

    public void onConnect() { /* Place code here */ }

    public void onDisconnect() { /* Place code here */ }

    public void onError(Exception e) { /* Place code here */ }

});
```

{% hint style="info" %}
The `ConnectionEventListener` interface utilizes default methods, which enables us to override only the methods we wish to implement ourselves and ignore the rest.
{% endhint %}

### C# SDK

For the C# SDK we utilize `EventHandler` from the .NET standard library for raising events related to the service's internal state. The example code block below shows how these handlers may be used with lambda expressions.

```csharp
service.Connected += (sender, args) => { /* Place code here */ };

service.Disconnected += (sender, args) => { /* Place code here */ };

service.Error += (sender, exception) => { /* Place code here */ };
```

### C++ SDK

For the C++ SDK we utilize the function wrapper `std::function` from the standard library as our handler for notifications raised by the service. The example code block below shows how these handlers may be used with lambda expressions.

```cpp
service->set_connected_handler([]() { /* Place code here */ });

service->set_disconnected_handler([]() { /* Place code here */ });

service->set_error_handler([](const std::exception& e) { /* Place code here */ });
```
