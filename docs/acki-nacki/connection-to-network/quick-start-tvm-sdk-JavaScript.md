## **Prerequisites**

* Rust v1.76+  
* Node.js v18.19.1
* Python 3  
* Python 3 setuptools  
<!-- TODO giver to wallet -->
* [Wallet-contract](./create-giver.md) to be used for payment for deploying contract  
* Demo contract [`helloWorld.sol`](./create-and-compile-contract.md)  
* [Demo application](https://github.com/tvmlabs/sdk-examples/tree/main/apps/javascript/helloWorld)  


**This demo app implements the following scenario:**

1. Creates and initializes an instance of the SDK client;

2. Deploys the `helloWorld` contract:

    2.1 Generates key pair for the contract;

    2.2 Calculates future address of the contract;

    2.3 Sends to the future address of the contract some tokens required for deploy;

    2.4 Deploys the `helloWorld` contract;

3. Gets account info and print balance of the `helloWorld` contract

4. Runs account's get method `getTimestamp`

5. Executes `touch` method for newly deployed `helloWorld` contract

6. Runs contract's get method locally after account is updated

7. Sends some tokens from `helloWorld` contract to a random account


!!! warning "Important"

    **For the application to work, you should to place `ABI files` of the `wallet` and `helloWorld` contracts into the `contracts` folder.**

!!! info

    For testing your developed applications, you can use Acki Nacki development blockchain  
    at **ackinacki-testnet.tvmlabs.dev**  

    To replenish the balance of wallet-contract, please contact us in [Channel on Telegram](https://t.me/+1tWNH2okaPthMWU0).


We will do all the work in this quick start in a separate `~/test-sdk` folder.
Let's create it:

```
cd ~
mkdir test-sdk
```

## **Prepare SDK binding for JavaScript**


1.Clone the repository to a separate directory:  

```
cd ~/test-sdk
git clone https://github.com/tvmlabs/tvm-sdk-js.git
```

2.Run build:

```
cd tvm-sdk-js/packages/lib-node/build
cargo run
```

As a result, the builded binding `eversdk.node` will be placed into the folder `~/test-sdk/tv-sdk-js/packages/lib-node`.


## **Prepare demo application**


1.Clone repository contains the demo application:

```
cd ~/test-sdk
git clone https://github.com/tvmlabs/sdk-examples.git
cd sdk-examples/apps/javascript/helloWorld
```

2.By this point, you should have deployed a wallet from which the balances of your demo contracts will be replenished.  
You can do this by following [the instructions](./create-giver.md).


3.Configure wallet for using in the demo app:

For demo app working, you should configure the wallet.
To do this, in the demo folder, edit `.env` file with following content:

<!-- TODO rename giver to wallet -->

```
CONTRACT_CODE=PATH_TO_HELLOWORLD_CONTRACT_CODE    # helloWorld.tvc
GIVER_ADDRESS=YOUR_WALLET_ADDRESS
GIVER_KEYS=PATH_TO_YOUR_WALLET_KEYS_FILE
```

3.Install the packages `@eversdk/core` and `@eversdk/lib-node` for the demo application:

```
npm install --save @eversdk/core @eversdk/lib-node
```

4.Replace the binary file in `@eversdk/lib-node` with an Acki Nacki-compatible one, which was builded early:  

```
cp ~/test-sdk/tv-sdk-js/packages/lib-node/eversdk.node ~/test-sdk/gosh-examples/sdk/javascript/helloWorld/node_modules/@eversdk/lib-node/
```


## **Run it**

Go to the folder with the demo application and run it:

```
cd ~/test-sdk/gosh-examples/sdk/javascript/helloWorld
node index.js
```

You will see a result similar to the following:


```
giver keys fname: ../../../contracts/simpleWallet/giver.keys.json
Future address of helloWorld contract is: 0:c2ba017472be9e5ea043a38a51aa17aa931ffb76981320ba978eeded443cafde
Transfering 1000000000 tokens from giver to 0:c2ba017472be9e5ea043a38a51aa17aa931ffb76981320ba978eeded443cafde
Success. Tokens were transfered

Deploying helloWorld contract
Success. Contract was deployed

helloWorld balance is 986483999
Run `getTimestamp` get method
`timestamp` value is {
  value0: '0x0000000000000000000000000000000000000000000000000000000066851f5d'
}
Calling touch function
Success. TransactionId is: 3afd14790d92e449d3f76f0de079efd2ec464438dc415077e85045261fe39c76

Waiting for account update
Success. Account was updated, it took 0 sec.

Run `getTimestamp` get method
Updated `timestamp` value is {
  value0: '0x0000000000000000000000000000000000000000000000000000000066851f60'
}
Sending 100000000 tokens to 0:d0d1ab370d669dcf715be4de9c80c7972ddd250636b2f97550ca9bed752880be
Success. Target account will recieve: 99000000 tokens

Normal exit
```


## **Source code**

The source code of all the components used can be found [here](https://github.com/gosh-sh/gosh-examples)




