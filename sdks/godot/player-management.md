# Player Management

## Getting Current Player

Below we demonstrate how to fetch the current user. This will only work when the TrustedPlatformClient is authenticated with a player access token, as such this query is more relevant on the client-side. If you need to fetch a player on the server you can explicitly define the id or name of the player.

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _get_current_player_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _get_current_player_cb = EnjinCallback.new(self, "_get_current_player")

func get_current_player():
   _client.user_service().get_user(GetUserInput.new(), { "callback": _get_current_player_cb })

func _get_current_player(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var user: Dictionary = gql.get_result()
```
{% endtab %}
{% endtabs %}

## Getting Player Identities

The example below demonstrates how to include the player identities in the user query:

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _get_player_identities_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _get_player_identities_cb = EnjinCallback.new(self, "_get_player_identities")

func get_player_identities(name: String):
   var input: GetUserInput = GetUserInput.new().name(name)
   input.user_i.with_identities(true)
   _client.user_service.get_user(input, { "callback": _get_player_identities_cb })

func _get_player_identities(udata: Dictionary):
   pass
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var user: Dictionary = gql.get_result()
   var identities: Array = user.identities
```
{% endtab %}
{% endtabs %}

## Linking A Player

While it is possible to explicitly link an Ethereum address to identity in the SDK, we recommend displaying the linking code or linking code QR to the player's so that they can link from within the Enjin Wallet Android or iOS app. Below we demonstrate how to get the linking code and QR URL:

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _get_identity_code_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _get_player_identities_cb = EnjinCallback.new(self, "_get_player_identities")

func get_identity_code():
   var input: GetUserInput = GetUserInput.new()
   input.user_i.with_identities(true)
   input.identity_i.with_linking_code(true)
   input.identity_i.with_linking_code_qr(true)
   _client.user_service.get_user(input, { "callback": _get_identity_code_cb })

func _get_identity_code_cb(udata: Dictionary):
   pass
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var user: Dictionary = gql.get_result()
   var identity: Dictionary = user.identities[0]
   var text_code = identity.linkingCode
   var qr_code_url = identity.linkingCodeQr
```
{% endtab %}
{% endtabs %}

## Getting Player Balances

There are various ways to get player balances. We highly recommend using the wallet service to explicitly fetch balances for an Ethereum address. By doing so you can limit the scope of data returned in the response compared to other approaches. For demonstration purposes we will show how to include balances when fetching a player as well as how to fetch the wallet for a specific Ethereum address:

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _get_balances_cb: EnjinCallback
var _get_wallet_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _get_balances_cb = EnjinCallback.new(self, "_get_balances")
   _get_wallet_cb = EnjinCallback.new(self, "_get_wallet")

func get_balances():
   var input: GetUserInput = GetUserInput.new()
   input.user_i.with_identities(true)
   input.identity_i.with_wallet(true)
   input.wallet_input.with_balances(true)
   _client.user_service.get_user(input, { "callback": _get_balances_cb })

func get_wallet(eth_addr: String):
   var input: GetWalletInput = GetWalletInput.new().eth_addr(eth_addr)
   input.wallet_i.with_balances(true)
   _client.wallet_service.get_wallet(input, { "callback": _get_wallet_cb })

func _get_balances_cb(udata: Dictionary):
   pass
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var user: Dictionary = gql.get_result()
   var identity: Dictionary = user.identities[0]
   var wallet: Dictionary = identity.wallet
   var balances: Array = wallet.balances
   for balance in balances:
       print("id: %s, index: %s, amount: %s" % [balance.id, balance.index, balance.value])

func _get_wallet_cb(udata: Dictionary):
   pass
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var user: Dictionary = gql.get_result()
   var identity: Dictionary = user.identities[0]
   var wallet: Dictionary = identity.wallet
   var balances: Array = wallet.balances
   for balance in balances:
       print("id: %s, index: %s, amount: %s" % [balance.id, balance.index, balance.value])
```
{% endtab %}
{% endtabs %}

