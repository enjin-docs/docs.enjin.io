---
description: Daemon Usage
---

# Daemon Usage

## Files

### **Storage**

The Wallet Daemon storage file is located in the following folder:

* Windows: `%LOCALAPPDATA%\enjin-wallet-daemon\storage.json`
* macOS: `$HOME\enjin-wallet-daemon\storage.json`
* Linux: `$HOME\enjin-wallet-daemon\storage.json`

### **Logs**

All Wallet Daemon activity is logged in the following files:

* Windows: `%LOCALAPPDATA%\enjin-wallet-daemon\enjin-wallet-daemon-<DATE>.json`
* macOS: `$HOME\enjin-wallet-daemon\enjin-wallet-daemon-<DATE>.json`
* Linux: `$HOME\enjin-wallet-daemon\enjin-wallet-daemon-<DATE>.json`

### Command-List

* `account new`
* `account import <PRIVATE KEY>`
* `link <CODE>`
* `run`
* `backup <FILENAME>`
* `decrypt`
* `decrypt <FILENAME>`

### New Account

Create a new account for this wallet. The wallet _must_ not already have an address. If it does, this command will do nothing and you will get an error.

If you want to create a new wallet address, you have to move or rename the storage file first.

**Example:**

```bash
node src/main.js account new
```

### Import Wallet

This command takes a single argument: the private key to use with the wallet. The format of the private key must be a 160-bit hexadecimal string prefixed with 0x.

**Example:**

```bash
node src/main.js account import 0x37986485ee024917a6cb7748c60d5d58214c7ca6e9a1d5d3880e2d94983012b7
```

### Link

Connect the wallet daemon with your Enjin Platform identity. You can link with many different identities.

**Example:**

```bash
node src/main.js link B3DJF4
```

### **Run**

Start the wallet daemon. This is the default command if none is supplied. The application will keep running until it's stopped \(Ctrl-C\) or killed.

**Example:**

```bash
node src/main.js run
```

### Backup

Copy the current storage file to the specified location. The file remains safely encrypted.

**Example:**

```bash
node src/main.js backup C:\Users\User\enjin-wallet-daemon-backup.json
```

### Decrypt

Read an encrypted storage file and output its content to the console. If no storage file is specified, the default storage is read.

**Example\(s\):**

```bash
node src/main.js decrypt C:\Users\User\enjin-wallet-daemon-backup.json
node src/main.js decrypt
```

