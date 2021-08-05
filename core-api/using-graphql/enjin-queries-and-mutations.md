---
description: A list of all Enjin Queries and Mutations
---

# Enjin Queries & Mutations \(V.1\)

Querying is the way to ask for data, it’s similar to the GET action in REST-based APIs.

Here is a list of the Enjin object types you can query through the API:

* **EnjinApp:** Use this query to get information about an app on the Enjin Platform.
* **EnjinApps:** Use this query to get information about multiple apps on the Enjin Platform.
* **EnjinBalances:** Use this query to get information about balances stored on the Enjin Platform.
* **EnjinIdentities:** Use this query to get information about identities stored on the Enjin Platform.
* **EnjinIdentity:** A user's identity for a game.
* **EnjinOauth:** Use this query to log users in and obtain oAuth access tokens.
* **EnjinPlatform:** Use this query to get information about a project on the Enjin Platform.
* **EnjinTokenEvents:** Use this to query the token events that has been recorded by the Enjin Platform.
* **EnjinToken:** Use this query to get token data.
* **EnjinTransactions:** Use this to query transaction requests.
* **EnjinUser:** Use this query to get information about a user on the Enjin Platform.
* **EnjinUsers:** Use this to query user data on the Enjin Platform.
* **EnjinWallet:** Use this query to get wallet data.

Mutating in GraphQL is the way to modify data, it is the term used to include all non-API functions other than GET. This includes functions such as PUT, POST, and DELETE that you may be familiar with from REST-based APIs.

Unlike querying, mutating requires adding all the arguments to the mutation. After it runs, you can query the values of the object after the mutation took place.

There are different types of Enjin object types that can be mutated through the API.

Here is a list of the Enjin object types that can be mutated:

* **CreateEnjinApp:** This mutation allows you to create a new project on the Enjin Platform.
* **UpdateEnjinApp:** This mutation allows you to update the details of a project such as the name or image.
* **DeleteEnjinApp:** This mutation allows you to delete a project from the Enjin Platform. This can only be performed by the project creator.
* **CreateEnjinIdentity:** This mutation allows you to create a new identity for users on the Enjin Platform.
* **UpdateEnjinIdentity:** This mutation allows you to update an identity. This mutation is also used to link a wallet with a signed message.
* **DeleteEnjinIdentity:** This mutation allows you to delete an identity from the Enjin Platform. You can also use this mutation to unlink an identity from a wallet.
* **CreateEnjinRequest:** This mutation allows you to create a new transaction request to send to the blockchain, and is the main way to interact with the different smart contract methods. When creating transaction requests, it is important to use the correct Identity ID as the ethereum address that is stored on it will be used as the 'creator' of the request and so needs to match the creator or owner of the token being manipulated. In the case of a Create request, the ID will become the 'creator' of the new token.
* **UpdateEnjinRequest:** This mutation allows you to update a pending transaction request that's not yet been signed and broadcast to the blockchain.
* **DeleteEnjinRequest:** This mutation allows you to cancel a transaction request that's not yet been signed and broadcast to the blockchain.
* **CreateEnjinUser:** This mutation allows you to create a player for your application on the Enjin Platform.
* **UnlinkApp:** This mutation allows you to unlink a wallet from a project.
* **UnlinkIdentity:** This mutation allows you to unlink a wallet from an identity.
* **InvalidateTokenMetadata:** Invalidate the metadata of a token instantly.

You can find comprehensive information about what data can be queried and mutated using these Object Types in the **GraphiQL Documentation Explorer.**

To find it, go to the [**GraphiQL visual interface**](https://cloud.enjin.io/graphiql) and click the _"Docs"_ button in the top-right corner.

### Querying Variables

You may notice in our documentation, we provide examples of our queries and mutations that you can use and they will often contain variables within them. You can query these variables by simply passing through the data in the "Query Variables" section at the bottom of the page.

Simply slide up the bottom-bar \(Query Variables\) and begin inputting the variables and their respective data.

![Enjin Linking Platform](https://assets-global.website-files.com/5d56cb37dc00727a4f69850c/5ffb6dae0d861daea4ea4c02_querying_using_variables.png)

### Browsing the Schema

On the right side, there should be a documentation panel to expand and browse for all the requests and parameters you can use. See [here](https://graphql.org/learn/queries/) for documentation on Queries and Mutations. Queries are requests for information from the server, where Mutations are requests that modify server-side data.

### Making a Request

On the \(top\) left panel, you would enter in your request to be made to the Enjin Cloud. Press the “Play” button at the top to submit that request, and you will receive a response on the right panel, sometimes a notification will appear in your dev wallet to sign a transaction depending on the request made.

