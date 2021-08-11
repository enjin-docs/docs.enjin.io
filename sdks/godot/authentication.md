# Authentication

### Project Authentication

The example below demonstrates how to authenticate a server client with the project id and secret.

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _auth_app_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _auth_app_cb = EnjinCallback.new(self, "_auth_app")

func auth_app(app_id: int, app_secret: String):
   _client.auth_service().auth_app(app_id, app_secret, { "callback": _auth_app_cb })

func _auth_app(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   print("App Authenticated!")
```
{% endtab %}
{% endtabs %}

### Player Authentication

Once the server client has been authenticated, you can get a player access token as seen in the example below. The player access token should then be forwarded to the player client.

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _auth_player_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _auth_app_cb = EnjinCallback.new(self, "_auth_player")

func auth_player(player_name: String):
   _client.auth_service().auth_player(player_name, { "callback": _auth_player_cb })

func _auth_player(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var result: Dictionary = gql.get_result()
   var player_access_token = result.accessToken
```
{% endtab %}
{% endtabs %}



