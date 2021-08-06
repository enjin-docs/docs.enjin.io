---
description: Learn how to create your player and link your wallet to get started
---

# Creating your Player

Verify your wallet address so it can approve blockchain transactions sent from your project.

### **Step 1: Create your User**

To run processes that need to be approved by your developer wallet, you will need to create yourself an account/player. Select a username and hit the "Play" button on GraphiQL's Playground. 

```graphql
mutation {
  CreatePlayer(id: "Your Username") {
    accessToken
  }
}
```

Using this query should return a unique Access Token for yourself. You will want to keep this Access Token server-side, and somewhere stored securely.

### Step 2: Link Your Wallet

From your account that you've generated from the previous step, you will want to link your project to your developer wallet. You can link your wallet and retrieve linking information by using the following query:

```graphql
{
  GetPlayer(id: "Your Username") {
    id
    wallet {
      ethAddress
    }
    linkingInfo {
      code
      qr
    }
    createdAt
    updatedAt
  }
}
```

Using the query above should return information such as your username, your wallet address \(if already linked\), your `linkingInfo` with the option to link with the unique code, or via QR. 

* **Code:** You can link your wallet by going to the Enjin Wallet -&gt; Linked Projects -&gt; "+ Link Project" -&gt; Select your Developer Wallet and enter the unique code to link. 
* **QR:** You can link your wallet by going to the Enjin Wallet -&gt; Linked Projects -&gt; "+ Link Project" -&gt; Select your Developer Wallet and scan the unique QR code that you've been provided. 

Once you have linked your wallet to your project, you will be able to approve and process any request from the Enjin Platform and Enjin API that are programmatically sent from your project. 

