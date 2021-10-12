# Linking a Player's Wallet

## Goal

Create a user account and link a wallet address to it, this will verify the user's ownership of the wallet address.

## Process

### **Step 1**

Create an Enjin identity for the user by running this query

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
mutation addUser {
  CreateEnjinUser(name: "Name here") {
      id
      accessTokens
      identities {
          linkingCode
          linkingCodeQr
       }
   }
 }
```
{% endtab %}

{% tab title="GraphQL V2" %}
```
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
_We recommend setting the username from your app as a static identifier from your existing database, so you always know how to reference the user’s Enjin identity._
{% endhint %}

### **Step 2**

The **addUser **query will return a linking code that you can display to the user. The user will scan the linking code with the Enjin Wallet and link their wallet to your platform.

Once the user is linked, you can run the following query to check their linking code or the details of their linked wallet.

{% tabs %}
{% tab title="GraphQL V1" %}
```graphql
query getUser {
  EnjinOauth(name:"<unique name for the user>") {
    id
    identities {
        wallet {
        ethAddress
     }
      linkingCode
      linkingCodeQr
    }
  }
}
```
{% endtab %}

{% tab title="GraphQL V2" %}
```
```
{% endtab %}
{% endtabs %}

### **Step 3**

Save the user’s Ethereum address, so you can query their wallet anytime you need to.
