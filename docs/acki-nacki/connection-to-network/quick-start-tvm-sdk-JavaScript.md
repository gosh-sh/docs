## **Prerequisites**

* Rust v.1.76+  
* Node.js v.18
* [Wallet-contract](./create-giver.md) to be used as a giver with keys  
* Contract, for example: [`helloWorld.sol`](./create-and-compile-contract.md)  
* [Demo application](https://github.com/gosh-sh/gosh-examples/tree/main/sdk/javascript/helloWorld)  


**This demo app implements the following logic:**

1. Creates and initializes an instance of the SDK client;

2. Deploys the `helloWorld` contract:

    3.1 Generates key pair for the contract;

    3.2 Calculates future address of the contract;

    3.3 Sends to the future address of the contract some tokens required for deploy;

    3.4 Deploys the `helloWorld` contract;

3. Gets account info and print balance of the `helloWorld` contract

4. Runs account's get method `getTimestamp`

5. Executes `touch` method for newly deployed `helloWorld` contract

6. Runs contract's get method locally after account is updated

7. Sends some tokens from `helloWorld` contract to a random account



!!! warning "Important"

    **For the application to work, you should to place `ABI files` of the `wallet` and `helloWorld` contracts in the `contracts` folder.**

!!! info

    For testing your developed applications, you can use Acki Nacki development blockchain  
    at **ackinacki-testnet.tvmlabs.dev**  

    To replenish the balance of wallet-contract, please contact us in [Channel on Telegram](https://t.me/+1tWNH2okaPthMWU0).


## **Setup giver**

Before you start, you should setup a wallet-contract to be used as a giver.  
Edit `.env` file with following content:

```
CONTRACT_CODE=PATH_TO_HELLOWORLD_CONTRACT_CODE    # helloWorld.tvc
GIVER_ADDRESS=YOUR_WALLET_ADDRESS
GIVER_KEYS=PATH_TO_YOUR_WALLET_KEYS_FILE
```

## **Preparation for work**

1. Install the packages `@eversdk/core` and `@eversdk/lib-node` for the Node.js application:

```
npm install --save @eversdk/core @eversdk/lib-node
```

2. Replace the binary file in `@eversdk/lib-node` with an Acki Nacki-compatible one:

2.1. Clone the repository to a separate directory:

```
git clone https://github.com/gosh-sh/ever-sdk-js
```

2.2. Switch to the "feature/masterchain-free" branch:

```
cd ever-sdk-js
git checkout feature/masterchain-free
```

3. Run the build:

```
cd packages/lib-node/build
cargo run
```

4. Copy the built file to the specified folder: `<YOUR_NODEJS_APP>/node_modules/@eversdk/lib-node`:

```
cp ../eversdk.node <YOUR_NODEJS_APP>/node_modules/@eversdk/lib-node/
```


## **Run it**

```
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




