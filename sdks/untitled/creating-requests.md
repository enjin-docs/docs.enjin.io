---
description: Learn more about creating requests with the Java SDK
---

# Creating Requests

 _**Note:** The below examples are in fact performing requests using KENJ rather than ENJ, due to the clients in those examples being built for the Kovan network and not the main network. You may use whichever network, such as Mainnet, JumpNet or Kovan._

### **ENJ Approval**

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.request.*;
import com.enjin.sdk.models.request.data.*;

public class ExampleServer {

   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void createRequest(Integer appId, int identityId) {
       ApproveEnjData data = ApproveEnjData.builder()
                                           .value(-1)
                                           .build();
       CreateRequest input = new CreateRequest().appId(appId)
                                                .identityId(identityId)
                                                .approveEnj(data);
       HttpResponse<GraphQLResponse> httpResponse = client.getRequestService().createRequestSync(input);<br><br>        if (!httpResponse.isEmpty()) {<br>            GraphQLResponse graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               Transaction transaction = graphQLResponse.getData();
           }
       }
   }
}
```

### Sending Tokens and ENJ

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.request.*;
import com.enjin.sdk.models.request.data.*;

public class ExampleServer {

   private TrustedPlatformClient client;

   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void sendEnj(Integer appId, int senderId, String to, String value) {
       SendEnjData data = SendEnjData.builder()
                                     .to(to)
                                     .value(value);
       CreateRequest input = new CreateRequest().appId(appId)
                                                .identityId(senderId)
                                                .sendEnj(data);
       HttpResponse<GraphQLResponse<CreateRequest>> httpResponse = client.getRequestService().createRequestSync(input);

       if (!httpResponse.isEmpty()) {
           GraphQLResponse<CreateRequest> graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               Transaction transaction = graphQLResponse.getData();
           }
       }
   }

   public void sendToken(Integer appId, int senderId, String to, String tokenId, Integer value) {
       SendTokenData data = SendTokenData.builder()
                                         .recipientAddress(to)
                                         .tokenId(tokenId)
                                         .value(value);
       CreateRequest input = new CreateRequest().appId(appId)
                                                .identityId(senderId)
                                                .sendToken(data);
       HttpResponse<GraphQLResponse<CreateRequest>> httpResponse = client.getRequestService().createRequestSync(input);

       if (!httpResponse.isEmpty()) {
           GraphQLResponse<CreateRequest> graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors) {
               Transaction transaction = graphQLResponse.getData();
           }
       }
   }
}
```

### Advanced Send

```java
import com.enjin.sdk.*;
import com.enjin.sdk.graphql.GraphQLResponse;
import com.enjin.sdk.http.HttpResponse;
import com.enjin.sdk.models.request.*;
import com.enjin.sdk.models.request.data.*;
import java.util.*;

public class ExampleServer {

   private TrustedPlatformClient client;
   
   public ExampleServer() {
       this.client = new TrustedPlatformClientBuilder().baseUrl(TrustedPlatformClientBuilder.KOVAN)
                                                       .build();
   }

   public void sendToken(Integer appId, Integer senderId, String[] toIds, String tokenId, String value) {
       List<TransferData> transfers = new ArrayList<TransferData>();

       for (String toId : toIds) {
           transfers.add(TransferData.builder()
                                     .fromId(senderId)
                                     .toId(toId)
                                     .tokenId(tokenId)
                                     .value(value)
                                     .build());
       }

       AdvancedSendTokenData data = AdvancedSendTokenData.builder()
                                                         .transfers(transfers)
                                                         .build();
       CreateRequest input = new CreateRequest().appId(appId)
                                                .identityId(senderId)
                                                .advancedSendToken(data);
       HttpResponse<GraphQLResponse<CreateRequest>> httpResponse = client.getRequestService().createRequestSync(input);

       if (!httpResponse.isEmpty()) {
           GraphQLResponse<CreateRequest> graphQLResponse = httpResponse.body();

           if (!graphQLResponse.hasErrors()) {
               Transaction transaction = graphQLResponse.getData();
           }
       }
   }
}
```



