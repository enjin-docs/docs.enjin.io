---
description: Learn more on how to get started with the Java SDK
---

# Introduction to Java SDK

The Java SDK requires at a minimum Java 8.

The source code for the Java SDK can be found [here](https://github.com/enjin/enjin-java-sdk) and the Java Documentation can be found [here](https://enjin.github.io/enjin-java-sdk/sdk/latest/).

### Downloading the SDK

#### **Maven**

```markup
<dependency>
 <groupId>com.enjin</groupId>
 <artifactId>blockchain-sdk</artifactId>
 <version>1.0.1</version>
</dependency>
```

**Gradle**

```groovy
dependencies {
   implementation 'com.enjin:blockchain-sdk:1.0.1'
}
```

**Git**

For those that don't use Maven or Gradle, you can manually build the Java SDK and add it to your project**'**s classpath.

1. Clone the Java SDK [repository](https://github.com/enjin/enjin-java-sdk) using git.
2. Initialize git modules: `git submodule init`
3. Build the Java SDK: "./gradlew sdk:build" \(Linux\) or "./gradlew.bat sdk:build" \(Windows\).
4. Navigate to the `build/libs` folder in the sdk module.
5. Add the jar ending in `-all` to your project's classpath.

### Set-up and Run SDK Example

**Create Example Project**

1. [Register](https://enjin.io/platform-signup) on the Enjin Platform if you have not done so already.
2. Select `Create Project` from the `Platform` page.
3. Set the project a name, description and image.
4. Click `Save Changes` to create your project.

**Create Example Assets**

1. Open your project by selecting it from the `Platform` page.
2. Go to `Assets` and click `Create Asset`.
   1. Note: If you are having trouble creating your asset, you can check [here](https://enjin.io/help/creating-your-first-blockchain-asset) on how to create your digital assets.
3. Set the name, total supply, value per asset, ENJ returned on melt, and the starting supply. All other settings can be left as the default.
4. Click `Create Asset`.

**Configuring the Example**

Next**,** we need the required details to use for our project. You will need the ID of the identity linked to your wallet, the ID and secret of the project you created, and the IDs of the assets you created.

**Getting the Project ID and Secret**

 To get the ID and secret of the project you created, you can go [here](https://cloud.enjin.io/graphql/playground) and execute the following query:

```graphql
query {
 EnjinUser {
   apps {
     id
     name
     secret
   }
 }
}
```

**Getting the Developer Identity ID**

The following query can be used to get the ID of the developer identity associated with your project:

```graphql
query {
 EnjinUser {
   identities {
     id
     appId
     wallet {
       ethAddress
     }
   }
 }
}
```

**Getting the Asset Token IDs**

You can find the token IDs of the assets you created by going to the assets tab of your project. The IDs are under the `Item ID` column.

