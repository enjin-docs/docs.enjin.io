---
description: Learn how to create a custom JSON metadata file
---

# Creating a Custom JSON File

If you wish to create your own Metadata file, you will need to save it as a .json file.

Once you have your .json file uploaded with public read access, you can make the request to set the item URI \(Uniform Resource Identifier\).

 Here is an example of a simple metadata schema:

```graphql
{ 
 "name": "item_name",
 "description": "Description line 1.\nDescription line2.",
 "image": "/image.jpg"
}
```

For more information on how to create a more robust JSON file, visit the [ERC-1155 Github](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1155.md#erc-1155-metadata-uri-json-schema).

### Specific Metadata URI

Any token ID may have a metadata URI that can be retrieved by calling `uri(_id)` on the ERC-1155 contract.

If an individual Non-Fungible token ID has a metadata URI defined, client apps should use this URI. If not defined, client apps should `call uri(_id)` on the base token id to retrieve the Default URI for the entire set of Non-Fungible tokens.

### Default URI

A Non-Fungible token that defines a Default URI in its base token has the option of using an {id} placeholder in the URI itself. This will get replaced with the distinct ID when accessing NFTs.

**Example:**

> yoursite.com/{id}.json -&gt; yoursite.com/bd4818c04f57a2ebc473d74ee06d6e0600000000000000000000000000000001.json

### **Images**

If the Default URI contains an image property that in turn contains the {id} placeholder, the image URL will be used as the default image for all tokens of this type.

> yoursite.com/images/{id}.jpg -&gt; yoursite.com/images/bd4818c04f57a2ebc473d74ee06d6e0600000000000000000000000000000001.jpg

The **image** property can also be a static URI without the placeholder, as desired.

### Setting asset backgrounds

If you opt for generating your own metadata, in the JSON you can set various coloured backgrounds for your assets to display in the Enjin Wallet app. 

To do this, you will need to set the `color`: attribute in your JSON file, such as the following example:

{% tabs %}
{% tab title="JSON" %}
```graphql
{
  "name": "John Wick",
  "description": "My name is John Wick",
  "image": "image url",
  "color": "teal"
}
```
{% endtab %}
{% endtabs %}

You can set the following colours:

* grey =&gt; \#616266 
* purple =&gt; \#5b3cb6 
* green =&gt; \#477b19 
* blue =&gt; \#3761a8 
* orange =&gt; \#9b6132 
* pink =&gt; \#993b9a 
* teal =&gt; \#3b7e9a 
* red =&gt; \#9a3b3b

### Setting asset properties

If you are interested to set unique properties to your assets, you can do this via your custom JSON file. 

To do this, you will need to set the `properties` attribute in your JSON file, such as the following example:

{% tabs %}
{% tab title="JSON" %}
```graphql
{
  "name": "John Wick",
  "description": "My name is John Wick",
  "image": "image url",
  "properties": {
    "Multiverse": "A magical land"
}
```
{% endtab %}
{% endtabs %}

You can set as many different properties as you'd like. Once set, these unique properties will display on your asset in the Enjin Wallet app, and on EnjinX.

