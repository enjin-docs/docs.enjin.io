---
description: Learn how to get started with the Enjin Wallet Daemon.
---

# Daemon First Steps

The Enjin Wallet Daemon is a utility that manages an Ethereum address linked to an Enjin Trusted Cloud identity. When a transaction is submitted on the Enjin Platform, the wallet daemon receives that transaction, signs it, and sends it back to the Trusted Cloud.

### Enjin Wallet Daemon Configuration

Before initializing the Wallet Daemon, open your enjin-wallet-daemon.1.x.x-beta folder and search for the example-config.json file, the contents of this file features some basic configuration parameters.

Copy the file from example-config.json to config.json and then open it in a text editor.

```text
{
   "salt": "193e9997-5a10-4d9e-a829-69ddcf6cbf70",
   "keyIterations": 1000,
   "chain": "kovan",
   "enjinxEndpoint": "https://daemon.api.enjinx.io/",
   "minGasPrice": 1000000000,
   "maxGasPrice": 21000000000
}
```

"`salt": "193e9997-5a10-4d9e-a829-69ddcf6cbf70`" - This paramater is used when encrypting/decrypting your daemon password. For improved security, you can set the salt to anything else \(such as a different UUID4 string\).

`"chain"`: `"kovan"`, `"mainnet"` , `"jumpnet"`- This parameter defines which network you are going to be running your wallet daemon on.

`"minGasPrice"` and `"maxGasPrice"` - Both parameters refer to ETH gas prices and can be used to constrain the minimum and maximum amount of gas to be used when signing a transaction.

### New Wallet Creation

This is the recommended way to initialize a Wallet Daemon.

Run node src/main.js account new  
Notice the new wallet address is printed on the console.

**Keep a backup of your password somewhere safe! Otherwise, there is no way to recover your account.**

### Import Existing Private Key

**From Enjin Wallet**

The Enjin Wallet uses the Ledger \(ETH\) _HD derivation path_ \(`m/44'/60'/0'`\). You can use MyEtherWallet to rebuild your private key from the 12-word recovery phrase.

This method is _rather insecure_ and should only be used knowing that it exposes your private key to a website that could have been compromised. To mitigate the risk, it's highly recommended to deploy a private copy of MyEtherWallet from [https://github.com/kvhnuke/etherwallet/releases](https://github.com/kvhnuke/etherwallet/releases)

If you decide to go this route, click on "View Wallet Info" and follow the onscreen instructions:

* Mnemonic Phrase
* Pasting your 12 words and keeping the password field empty
* Selecting the _Ledger \(ETH\)_ derivation path
* Choosing the correct address from the suggestion list

**From MetaMask**

Go into account details and select "Export Private Key"

**From Parity/Geth**

Assuming your client installation uses the default data folders, the keys are stored there:

**Parity**

* Windows: `%HOMEPATH%/AppData/Roaming/Parity/Ethereum/keys`
* macOS: `~/Library/Application\ Support/io.parity.ethereum/keys`
* Linux: `$HOME/.local/share/io.parity.ethereum/keys`

**Geth**

* Windows: `%APPDATA%\Ethereum\keystore`
* macOS: `~/Library/Ethereum/keystore`
* Linux: `~/.ethereum/keystore`

Each key is stored in an extensionless json file. Here again, you can use "MyEtherWallet" to extract the private keys.

This method is _rather insecure_ and should only be used knowing that it exposes your private key to a website that could have been compromised. To mitigate the risk, it's highly recommended to deploy a private copy of MyEtherWallet from [https://github.com/kvhnuke/etherwallet/releases](https://github.com/kvhnuke/etherwallet/releases)

If you decide to go this route, click on "View Wallet Info" and follow the onscreen instructions:

* Keystore / JSON File
* Select your file, enter your password

#### Link To the Enjin Platform

1. Create an account on the Enjin Platform.
   1. Mainnet: cloud.enjin.io
   2. JumpNet: jumpnet.cloud.enjin.io
   3. Kovan: kovan.cloud.enjin.io
2. Create an identity for the application you want to control with the wallet daemon.
3. Copy the linking code from the identity `<CODE>`.
4. Run node src/main.js link `<CODE>`

#### Run The Wallet Daemon

Run `node src/main.js`.

