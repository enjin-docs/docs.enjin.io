# Message Logging

{% hint style="info" %}
## Alpha Documentation

The documentation for the Enjin SDKs pertain to the Project and Player schemas which are currently in an **Alpha** release. The Project and Player schemas are **not yet publicly available** and therefore this documentation is limited only to those who already have access. For any queries, please contact [Enjin Support](mailto:support@enjin.io).
{% endhint %}

## Logger

### ILogger Interface

For logging the SDKs define a `ILogger` interface that provides a common API for their logging purposes.

### Built-in Logger

Each SDK comes with a built-in `Logger` class that implements the `ILogger` interface. These loggers offer basic functionality that allow us to jump into using logging features without dedicating too much time to develop our own implementation first.

## Message Levels

For logging the SDKs define six levels that messages may be logged on. These log levels are:

* `TRACE`
* `DEBUG`
* `INFO`
* `WARN`
* `ERROR`/`ERR`
* `SEVERE`

## Logger Provider

The `LoggerProvider` is the highest level class that we interact with when utilizing a SDKs logging functions. The `LoggerProvider` allows components within the SDKs to share log settings and resources if we desire and in turn helps us save resources as well.

To use the `LoggerProvider` we must pass it an instance of a class implementing the `ILogger` interface, such as the `Logger` class built into the SDKs as shown in the example below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.utils.Logger;
import com.enjin.sdk.utils.LoggerProvider;

Logger logger = new Logger();

LoggerProvider provider = new LoggerProvider(logger);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Utils;

Logger logger = new Logger();

LoggerProvider provider = new LoggerProvider(logger);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/Logger.hpp"
#include "enjinsdk/LoggerProvider.hpp"
#include <memory>

using namespace enjin::sdk::utils;

std::shared_ptr<Logger> logger = std::make_shared<Logger>();

std::shared_ptr<LoggerProvider> provider = std::make_shared<LoggerProvider>(logger);
```
{% endtab %}
{% endtabs %}

When creating the `LoggerProvider` we may also choose to define the default message level and the default debug level it calls the logger on as shown in the example below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.utils.LogLevel;
import com.enjin.sdk.utils.LoggerProvider;

LogLevel message = LogLevel.WARN;
LogLevel debug = LogLevel.ERROR;

// With a defined ILogger instance
new LoggerProvider(logger, message, debug);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK.Utils;

LogLevel message = LogLevel.WARN;
LogLevel debug = LogLevel.ERROR;

// With a defined ILogger instance
new LoggerProvider(logger, message, debug);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/ILogger.hpp"
#include "enjinsdk/LoggerProvider.hpp"
#include <memory>

using namespace enjin::sdk::utils;

LogLevel message = LogLevel::WARN;
LogLevel debug = LogLevel::ERR;

// With a defined ILogger instance
std::make_shared<LoggerProvider>(logger, message, debug);
```
{% endtab %}
{% endtabs %}

By default the `LoggerProvider` sets the message level to `INFO` and the debug level to `DEBUG` if we do not define them ourselves.

We may pass the `LoggerProvider` to top level SDK class that accept it, such as the `ProjectClient` as can be seen below:

{% tabs %}
{% tab title="Java" %}
```java
import com.enjin.sdk.ProjectClient;

ProjectClient client = new ProjectClient("<enjin-host-uri>", true, provider);
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using Enjin.SDK;

ProjectClient client = new ProjectClient("<enjin-host-uri>", provider);
```
{% endtab %}

{% tab title="C++" %}
```cpp
#include "enjinsdk/ProjectClient.hpp"
#include <memory>

using namespace enjin::sdk;

std::unique_ptr<ProjectClient> client = ProjectClientBuilder()
            .base_uri("<enjin-host-uri>")
            .logger_provider(provider)
            .build();
```
{% endtab %}
{% endtabs %}

