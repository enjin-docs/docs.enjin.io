# Creating Requests

## ENJ Approval

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _create_request_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _create_request_cb = EnjinCallback.new(self, "_create_request")

func create_reqeust(app_id: int, identity_id: int):
   var input = CreateRequestInput.new()
   input.app_id(app_id)
   input.identity_id(identity_id)
   input.tx_type("APPROVE")
   input.approve_enj({ "value": -1 })
   _client.request_service().create_request(input, { "callback": _create_request_cb })

func _create_request(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var request: Dictionary = gql.get_result()
```
{% endtab %}
{% endtabs %}

## Sending Tokens And ENJ

{% tabs %}
{% tab title="GDScript" %}
```java
var _client: TrustedPlatformClient
var _create_request_cb: EnjinCallback

func _init():
   _client = TrustedPlatformClient.new()
   _create_request_cb = EnjinCallback.new(self, "_create_request")

func send_token(app_id: int, sender_id: int, recipient_id: int, token_id: String, amount: int):
   var input = CreateRequestInput.new()
   input.app_id(app_id)
   input.identity_id(sender_id)
   input.tx_type("SEND")
   input.send_token({ "token_id": token_id, "recipient_identity_id": recipient_id, "value": amount })
   _client.request_service().create_request(input, { "callback": _create_request_cb })

func send_enj(app_id: int, sender_id: int, recpient_addr: String, amount: String):
   var input = CreateRequestInput.new()
   input.app_id(app_id)
   input.identity_id(sender_id)
   input.tx_type("SEND_ENJ")
   input.send_enj({ "to": recipient_addr, "value": amount})
   _client.request_service().create_request(input, { "callback": _create_request_cb })

func _create_request(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var request: Dictionary = gql.get_result()
```
{% endtab %}
{% endtabs %}

## Advanced Send

{% tabs %}
{% tab title="GDScript" %}
```java
func _init():
   _client = TrustedPlatformClient.new()
   _create_request_cb = EnjinCallback.new(self, "_create_request")

func send_token(app_id: int, sender_id: int, recipient_ids: Array, token_id: String, amount: int):
   var input = CreateRequestInput.new()
   input.app_id(app_id)
   input.identity_id(sender_id)
   input.tx_type("SEND")
   var transfers: Array = []
   for id in recipient_ids:
       transfers[transfers.size() - 1] = { "from_id": sender_id, "to_id": id, "token_id": token_id, "value": amount }
   input.advanced_send_token({ "transfers": transfers})
   _client.request_service().create_request(input, { "callback": _create_request_cb })

func _create_request(udata: Dictionary):
   var gql: EnjinGraphqlResponse = udata.gql
   if gql.has_errors() or not gql.has_result():
       return
   var request: Dictionary = gql.get_result()
```
{% endtab %}
{% endtabs %}



