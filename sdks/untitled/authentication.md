---
description: Learn how to authentication your project and player
---

# Authentication

### Project Authentication

The example below demonstrates how to synchronously authenticate a server-client with the project's ID and secret.

```java
import com.enjin.sdk.*;

public class ExampleServer {

   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public boolean authApp(int appId, String appSecret) {
       this.client.authAppSync(appId, appSecret);
       
       return client.isAuthenticated();
   }
}
```

### Player Authentication

Once the server-client has been authenticated you can get a player access token as seen in the example below. The player access token should then be forwarded to the player client.

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.AccessToken;
import com.enjin.sdk.models.user.*;

public class ExampleServer {
   
   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void authPlayer(String id) {
       AuthPlayer input = new AuthPlayer().id(id);
       HttpResponse<GraphQLResponse> httpResponse = client.getUserService().authUserSync(input);<br><br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               AccessToken accessToken = graphQLResponse.getData();
           }
       }
   }
}
```



