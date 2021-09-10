# Handling Platform Events

### TODO

TODO

### Registering a Event Listener

TODO: Register and check if registered

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.events.NotificationListener;
import com.enjin.sdk.events.NotificationListenerRegistration;
import com.enjin.sdk.models.NotificationEvent;

class Listener implements NotificationListener {

    public void notificationReceived(NotificationEvent event) {
        // Your code here
    }

}

NotificationListenerRegistration reg = service.registerListener(new Listener());
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Events;
using Enjin.SDK.Models;

class Listener : IEventListener
{

    public void NotificationReceived(NotificationEvent notificationEvent)
    {
        // Your code here
    }

}

EventListenerRegistration reg = service.RegisterListener(new Listener());
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/EventListenerRegistration.hpp"
#include "enjinsdk/IEventListener.hpp"
#include "enjinsdk/models/NotificationEvent.hpp"
#include <memory>

using namespace enjin::sdk::events;
using namespace enjin::sdk::models;

class Listener : public IEventListener {
public:

    void notification_received(const NotificationEvent& event) override {
        // Your code here
    }

};

std::shared_ptr<Listener> listener = std::make_shared<Listener>();

EventListenerRegistration reg = service->register_listener(listener);
```
{% endtab %}
{% endtabs %}

TODO: Unregister

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

### Subscribing to a Event Channel

TODO: Subscribe and check if subscribed

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

TODO: Unsubscribe

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

TODO: Additional details \(ie. automatic resubscription\)

### Matching Listeners for Events

TODO

#### Functional Matcher

TODO

{% tabs %}
{% tab title="Java" %}
```java
service.registerListenerWithMatcher(listener, notificationEvent -> {
    // Your code here

    return true;
}); // Returns listener registration
```
{% endtab %}

{% tab title="C\#" %}
```csharp
service.RegisterListenerWithMatcher(listener, eventType => {
    // Your code here

    return true;
}); // Returns listener registration
```
{% endtab %}

{% tab title="C++" %}
```cpp
service->register_listener_with_matcher(listener, [](EventType type) {
    // Your code here
    
    return true;
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

#### Including Events

TODO

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

service->register_listener_including_types(listener, {
    EventType::ASSET_MELTED,
    EventType::ASSET_MINTED,
    EventType::ASSET_TRANSFERRED
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

#### Excluding Events

TODO

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

service->register_listener_excluding_types(listener, {
    EventType::ASSET_MELTED,
    EventType::ASSET_MINTED,
    EventType::ASSET_TRANSFERRED
}); // Returns listener registration
```
{% endtab %}
{% endtabs %}

#### Java SDK Annotation

TODO

```java
import com.enjin.sdk.events.EventFilter;

@EventFilter({ /* Event types here */ })
Listener implements NotificationListener { /* ... */ }
```

