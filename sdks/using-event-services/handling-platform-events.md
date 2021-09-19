# Handling Cloud Events

## Creating a Event Listener

For us to be notified when our event service receives an event from the cloud we must provide it with a event listener for it to relay to. The SDKs provide an interface which we will use to implement a listener the service will use. An example of how we may implement the event listener interface can be seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.NotificationListener;
import com.enjin.sdk.models.NotificationEvent;

class Listener implements NotificationListener {

    public void notificationReceived(NotificationEvent event) {
        // Place code here
    }

}
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;
using Enjin.SDK.Models;

class Listener : IEventListener {

    public void NotificationReceived(NotificationEvent notificationEvent) {
        // Place code here
    }

}
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/IEventListener.hpp"
#include "enjinsdk/models/NotificationEvent.hpp"

using namespace enjin::sdk::events;
using namespace enjin::sdk::models;

class Listener : public IEventListener {
public:

    void notification_received(const NotificationEvent& event) override {
        // Place code here
    }

};
```
{% endtab %}
{% endtabs %}

The `NotificationEvent` argument in the notification received method models a event that the event service has received and parsed. This argument will contain information telling us the type of the event that was received, the channel the event was broadcasted on, and the serialized JSON message that is the data associated with the event, such as the asset ID for asset events or the wallet address for wallet events.

## Listener Registration

### Registering a Listener

With our event listener defined we can now instantiate it and register it with our event service. The event service has multiple registration methods with different functionality, but for now we will use the most basic of these methods. The basic registration method will register our listener and for any event the service receives and processes from the cloud our listener will receive the parsed event data. When registering our listener we will also get the listener registration object containing data about our registration.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.NotificationListenerRegistration;

NotificationListenerRegistration reg = service.registerListener(new Listener());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;

EventListenerRegistration reg = service.RegisterListener(new Listener());
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/EventListenerRegistration.hpp"
#include <memory>

using namespace enjin::sdk::events;

std::shared_ptr<Listener> listener = std::make_shared<Listener>();

EventListenerRegistration reg = service->register_listener(listener);
```
{% endtab %}
{% endtabs %}

### Unregistering a Listener

If we wish to do so we may also unregister our listener from the service. To do so we pass our listener as an argument to the service's unregister method. In the event that we did not create a variable for our listener before registering it, we may use the reference that is stored in the registration that we received upon registration as shown below:

{% tabs %}
{% tab title="Java" %}
```java
// Using a listener registration
service.unregisterListener(reg.getListener());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
// Using a listener registration
service.UnregisterListener(reg.Listener);
```
{% endtab %}

{% tab title="C++" %}
```cpp
// Using a listener registration
service->unregister_listener(reg.get_listener());
```
{% endtab %}
{% endtabs %}

## Event Channel Subscription

### Subscribing to a Channel

To subscribe to one of the four event channels used by the cloud we must provide the identifier for it. See the code block below for what these identifiers are:

{% tabs %}
{% tab title="Java" %}
```java
service.subscribeToProject("<the-project's-uuid>");

service.subscribeToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.subscribeToAsset("<the-asset's-id>");

service.subscribeToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
service.SubscribeToProject("<the-project's-uuid>");

service.SubscribeToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.SubscribeToAsset("<the-asset's-id>");

service.SubscribeToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
service->subscribe_to_project("<the-project's-uuid>");

service->subscribe_to_player("<the-project's-uuid>", "<the-player's-id>");

service->subscribe_to_asset("<the-asset's-id>");

service->subscribe_to_wallet("<the-wallet's-address>");
```
{% endtab %}
{% endtabs %}

After subscribing to a channel our event service will now receive events which are broadcasted on the specified event channel.

{% hint style="warning" %}
When using the `PusherEventService` subscribed channels may only be subscribed to after starting the service for the first time.
{% endhint %}

We may also check to see if our service is already subscribed to a particular event channel by using the appropriate method and passing the identifiers as shown below:

{% tabs %}
{% tab title="Java" %}
```java
service.isSubscribedToProject("<the-project's-uuid>");

service.isSubscribedToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.isSubscribedToAsset("<the-asset's-id>");

service.isSubscribedToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
service.IsSubscribedToProject("<the-project's-uuid>");

service.IsSubscribedToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.IsSubscribedToAsset("<the-asset's-id>");

service.IsSubscribedToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
service->is_subscribed_to_project("<the-project's-uuid>");

service->is_subscribed_to_player("<the-project's-uuid>", "<the-player's-id>");

service->is_subscribed_to_asset("<the-asset's-id>");

service->is_subscribed_to_wallet("<the-wallet's-address>");
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Channel subscriptions on the `PusherEventService` persist after shutting down and restarting the service.
{% endhint %}

### Unsubscribing from a Channel

To unsubscribe our service from a channel we will need to recall the information we provided when we first subscribed and provide it to the service's unsubscribe method as well. After doing so our service will no longer receive events from the cloud for the specified channel.

{% tabs %}
{% tab title="Java" %}
```java
service.unsubscribeToProject("<the-project's-uuid>");

service.unsubscribeToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.unsubscribeToAsset("<the-asset's-id>");

service.unsubscribeToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C\#" %}
```csharp
service.UnsubscribeToProject("<the-project's-uuid>");

service.UnsubscribeToPlayer("<the-project's-uuid>", "<the-player's-id>");

service.UnsubscribeToAsset("<the-asset's-id>");

service.UnsubscribeToWallet("<the-wallet's-address>");
```
{% endtab %}

{% tab title="C++" %}
```cpp
service->unsubscribe_to_project("<the-project's-uuid>");

service->unsubscribe_to_player("<the-project's-uuid>", "<the-player's-id>");

service->unsubscribe_to_asset("<the-asset's-id>");

service->unsubscribe_to_wallet("<the-wallet's-address>");
```
{% endtab %}
{% endtabs %}

## Matching Listeners for Events

In the case where we would like to register a more specialized event listener that only receives particular event types we may use a various means to specify which events we want to receive to offload responsibility of filtering events from our listener to the event service instead.

### Functional Matcher

For registering our listener in the service to process events under tailored conditions we specify, we may use the service's method for registering with a paired matcher for our listener. If the matcher returns `true`, then the service will pass the `NotificationEvent` to our listener for processing, whereas if the matcher returns `false`, then our listener will not receive the event. As with standard registration, this method returns a listener registration object.

{% tabs %}
{% tab title="Java" %}
```java
service.registerListenerWithMatcher(listener, notificationEvent -> {
    // Place code here

    return true;
}); // Returns listener registration
```
{% endtab %}

{% tab title="C\#" %}
```csharp
service.RegisterListenerWithMatcher(listener, eventType => {
    // Place code here

    return true;
}); // Returns listener registration
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/EventType.hpp"

using namespace enjin::sdk::models;

service->register_listener_with_matcher(listener, [](EventType type) {
    // Place code here

    return true;
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

### Including Events

For registering our listener in the service to process only a select set of events, we may use the service's method for registering with including event types. As with standard registration, this method returns a listener registration object.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.EventType;

service.registerListenerIncludingTypes(listener,
    EventType.ASSET_MELTED,
    EventType.ASSET_MINTED,
    EventType.ASSET_TRANSFERRED
); // Returns listener registration
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;

service.RegisterListenerIncludingTypes(listener,
    EventType.ASSET_MELTED,
    EventType.ASSET_MINTED,
    EventType.ASSET_TRANSFERRED
); // Returns listener registration
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/EventType.hpp"

using namespace enjin::sdk::models;

service->register_listener_including_types(listener, {
    EventType::ASSET_MELTED,
    EventType::ASSET_MINTED,
    EventType::ASSET_TRANSFERRED
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

### Excluding Events

For registering our listener in the service to not process a select set of events, we may use the service's method for registering with excluding event types. As with standard registration, this method returns a listener registration object.

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.models.EventType;

service.registerListenerExcludingTypes(listener,
    EventType.ASSET_MELTED,
    EventType.ASSET_MINTED,
    EventType.ASSET_TRANSFERRED
); // Returns listener registration
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;

service.RegisterListenerExcludingTypes(listener,
    EventType.ASSET_MELTED,
    EventType.ASSET_MINTED,
    EventType.ASSET_TRANSFERRED
); // Returns listener registration
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/models/EventType.hpp"

using namespace enjin::sdk::models;

service->register_listener_excluding_types(listener, {
    EventType::ASSET_MELTED,
    EventType::ASSET_MINTED,
    EventType::ASSET_TRANSFERRED
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

### Filtered Listener

We may also attach attributes/annotations on listener classes to indicate to the event service which events we want our listener to receive or to not receive. Generally, we can set which events we want the to filter for and also indicate if we want the filter allow or disallow said events. Examples for what this may look like in the SDKs which support this feature can be seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.EventFilter;
import com.enjin.sdk.events.NotificationListener;
import com.enjin.sdk.models.EventType;

@EventFilter(allow = true, value = {EventType.ASSET_MELTED /* more events */})
class Listener implements NotificationListener { /* ... */ }
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;
using Enjin.SDK.Models;

[EventFilter(allowed: true, EventType.ASSET_MELTED /* more events */)]
class Listener : IEventListener { /* ... */ }
```
{% endtab %}
{% endtabs %}

