---
description: Learn more on Player Management
---

# Player Management

### Getting the Current Player

Below we demonstrate how to fetch the current user. This will only work when `TrustedPlatformClient` is authenticated with a player access token. As such this query is more relevant on the client side. If you need to fetch a player on the server you can explicitly define the ID or name of the player.

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.user.*;

public class ExampleServer {
   
   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void getCurrentPlayer() {
       GetUser query = new GetUser().me();
       HttpResponse<GraphQLResponse> httpResponse = client.getUserService().getUserSync(query);<br><br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               User user = graphQLResponse.getData();
           }
       }
   }
}
```

### Getting Player Identities

The example below demonstrates how to include the player identities in the user query:

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.identity.*;
import com.enjin.sdk.models.user.*;
import java.util.List;

public class ExampleServer {
   
   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void getIdentities(String name) {
       GetUser query = new GetUser().name(name)
                                    .withUserIdentities(); // Includes the user identities
       HttpResponse<GraphQLResponse> httpResponse = client.getUserService().getUserSync(query);<br><br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               User           user       = graphQLResponse.getData();
               List<Identity> identities = user.getIdentities();
           }
       }
   }
}
```

### Linking a Player

While it is possible to explicitly link an Ethereum address to an identity in the SDK, we recommend displaying the linking code or linking code QR to the player so that they can link from within the Enjin Wallet. Below, we demonstrate how to get the linking code and QR URL:

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.identity.*;
import com.enjin.sdk.models.user.*;
import java.util.*;

public class ExampleServer {
   
   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void getIdentityCode(String name) {
       GetUser query = new GetUser().name(name)
                                    .withUserIdentities()
                                    .withLinkingCode()    // Includes the linking code and
                                    .withLinkingCodeQr(); // the qr url for the identities
       HttpResponse<GraphQLResponse> httpResponse = client.getUserService().getUserSync(query);<br><br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               User           user       = graphQLResponse.getData();
               List<Identity> identities = user.getIdentities();

               if (identities.size() > 0) {
                   Identity identity    = identities.get(0);
                   String   linkingCode = identity.getLinkingCode();
                   String   qrCodeUrl   = identity.getLinkingCodeQr();
               }
           }
       }
   }
}
```

### Getting Player Balances

There are various ways to get player balances. We highly recommend using the wallet service to explicitly fetch balances for an Ethereum address. By doing so you can limit the scope of data returned in the response compared to other approaches. 

For demonstration purposes, we will show how to include balances when fetching a player as well as how to fetch the wallet for a specific Ethereum address:

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.balance.*;
import com.enjin.sdk.models.identity.*;
import com.enjin.sdk.models.user.*;
import com.enjin.sdk.models.wallet.*;
import java.util.*;

public class ExampleServer {
   
   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   // Recommended approach
   public void getWallet(String ethAddr) {
       GetWallet query = new GetWallet().ethAddress(ethAddr)
                                        .withBalances(); // Includes the balances
       HttpResponse<GraphQLResponse> httpResponse = client.getWalletService().getWalletSync(query);<br>    <br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();
   
           if (!graphQLResponse.hasErrors()) {
               Wallet         wallet   = graphQLResponse.getData();
               List balances = wallet.getBalances();<br>            }<br>        }<br>    }<br><br>    public void getBalances(String name) {<br>        GetUser query = new GetUser().name(name)<br>                                     .withUserIdentities()<br>                                     .withWallet()    // Includes the wallet and<br>                                     .withBalances(); // the balances for it<br>        HttpResponse<GraphQLResponse<User>> httpResponse = client.getUserService().getUserSync(query);<br>    <br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse<User> graphQLResponse = httpResponse.body();<br>    <br>            if (!graphQLResponse.hasErrors()) {<br>                User           user       = graphQLResponse.getData();<br>                List<Identity> identities = user.getIdentities();<br>    <br>                if (identities.size() > 0) {<br>                    Identity       identity = identities.get(0);<br>                    Wallet         wallet   = identity.getWallet();<br>                    List balances = wallet.getBalances();
               }
           }
       }
   }
}
```

