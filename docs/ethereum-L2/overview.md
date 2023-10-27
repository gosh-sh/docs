# **Overview**


GOSH is an asynchronous, highly scalable validity rollup that enables any asset on the Ethereum blockchain to be transferred into GOSH and vice versa. All ZK Proofs (Zero-knowledge proofs) are prepared on the user side by a [**Proposer**](overview.md#definitions " is an off-chain program which packages all necessary data to prove to GOSH chain that a particular transaction (let’s call them “L2 transactions”) on Ethereum Network took place and vise versa — to prove to Ethereum ELOCK smart contract (i.e. Ethereum validators) that an L2 transaction took place on the GOSH Blockchain").
It is then submitted to the Independent Collator which receives user input and executes them on GOSH.

Anyone can submit a resulting **L2 (GOSH Blockchain)** state root to **L1 (Ethereum Blockchain)**.
Randomly selected Verifiers run the state transition periodically and slash Collators in case of fraud via decision by L1. Verifiers are slashed for false fraud alerts. If Collator is censoring users' transactions, it is possible to force the transaction via L1. 
Anyone can publish L2 state root but only Collator can propose L2 state change.

**Proof Summary**


| **What do we Prove**     | **How do we Prove it** |
| ------------------------ | ------------------------------------ |
| **`L1 Blocks are correct`**    | BLS Signatures check  |
| **`L2 Blocks are correct`**    | Validator signatures + Verifiers Fraud Proofs |
| **`L1 transaction are within the correct blocks`** | Merkle tree proof from Transaction hash to L1 block hash |
| **`L2 transaction are within the correct blocks`** | Merkle tree proof from Transaction hash to L2 block hash |
| **`All L1 transactions are provided to L2 from block A to block B`** | Txn count in block a and Txn count in block B are known we can verify that total transaction count transferred to [GLOCK](overview.md#contracts "is a special TIP-3 Token Root Contract on GOSH Blockchain") is correct and since we have hashes it's impossible to cheat
| **`Transaction counts and Balances are correct for L1 Block transmitted to L2`** | Merkle tree of account states for a particular L1 block |
| **`All L2 Withdrawal Transactions are transferred to L1   from Block A to Block B`** | Txn count in block a and Txn count in block B are known we can verify that total transaction count transferred to ELOCK is correct and since we have hashes it's impossible to cheat
| **`TIP-3 Deposit/Transfer/Withdrawal Transaction  Execution is correct`** | ZKP for TIP-3 Circuit |
| **`Validator set change from last KeyBlock is correct`** | ZKP for Elector contract Circuit |
| **`Validators Fraud Proofs`** | Fraud detection mechanism by Verifiers |





## **Roadmap**


### **Stage 1: Trustless Bridge**   (**In production**) ![](../images/green%20tick3.jpg)

**Challenges:**

* L1 can’t have the L2 entire state (L2 state is too large)
* There must be a mechanism to move funds from L2 even if: L2 is not moving; L2 has banned specific accounts
* EVM and TVM are different. TVM is a reference VM for the L2 chain. This means that even if L1 has a state it can’t execute transactions to verify correctness. But it can execute ZKP which will prove the correctness of operations in the particular circuit


!!! info
    At this stage we assume:  
    L2 fully trusts L1, it knows Validators (Committee) PubKeys and can always validate the chain of L1 blocks.  
    We do not validate the smart contract execution on L2. We protect against any malicious 3rd party except for L1 and L2 Validators.


As an example, we will talk about ETH moving from the Ethereum mainnet into WETH Asset on GOSH L2 Blockchain and back. In general, any asset on Ethereum can be supported with necessary adjustments made to [ELOCK](overview.md#contracts "is a GOSH L2 smart contract on Ethereum Blockchain") smart contract Deposit/Withdrawal functions.
Since GOSH uses ed25519 we use a double signature envelope scheme to prove signatures on GOSH to ELOCK Smart Contract on Ethereum (*we could use ZKP to prove the ed25519 or a precompile proposed EIP665 whenever either of those solutions will be production ready*).


!!! info 
    *What we don’t cover at this Stage?*  

    * L2 contract execution is not validated (no validity or fraud proofs)  
    * Funds retrieval function in case of L2 censored / stopped  
    * L1 Funds retrieval is complicated and expansive  



### **Stage 2: Optimistic roll-up**

!!! info
    At this stage we add fraud and execution proofs for [TIP-3](overview.md#definitions "is a distributed token smart contract standard on GOSH blockchain") contracts.

The Proposer constructs the TIP-3 execution proof and sends it together with block proofs. If the execution is correctly proved the funds can be withdrawn immediately. If the Proposer does not wish to pay the gas fees for ZKP execution it can supply the withdrawal request without any proof but with a bond. In which case the withholding period will be activated (hence optimistic rollup). Another Proposer can verify the correctness of execution of the TIP-3 in the proposed batch and if found incorrect execution can supply the fraud proof (consisting of proof of the correct execution of the corrupted TIP-3 transaction and proof of block tree hashes which will be incompatible with hashes provided by the first Proposer) and collect the Proposer Bond.
 
At this stage we have added a mechanism of Fraud proof of L2 validators making the network effectively on par with security assumptions of other optimistic rollups, but also providing a mechanism for immediate Validation of token contract execution on L2 network.

!!! info
    *What we don’t cover at this Stage?*  

    * Funds retrieval function in case of L2 censored/stopped  
    * L1 funds retrieval is complicated and expansive in case of immediate withdrawal  


### **Stage 3: Validium ZKP roll-up**


At this stage, we are adding external Verifiers and putting a bond of L2 Collators on the Ethereum mainnet. Verifiers will be able to supply fraud proofs as well as data availability proofs.

The Verifiers can slash the L2 Collators in case of misbehavior by supplying ZKPs proving the wrong block production, or by successfully challenging data availability proofs making it effectively an Ethereum Sharding design since GOSH is a multithreaded, multisharded blockchain.


!!! warning annotate "Important"
    At this stage, there is no need to trust L2 Collators with anything. L1 can verify all L2 state transitions and L2 can verify L1 contract state transitions. Funds are easily withdrawn from either blockchain. To break the system both L1 and L2 need to be corrupted or stopped simultaneously.


<!-- TODO -->
## **Contracts**


* **ELOCK** — is a GOSH L2 smart contract on Ethereum Blockchain. It receives deposits from users, manages withdrawals, and locks user funds. ELOCK also counts its total balance, and total transaction count and stores root Merkle proofs, withdrawal smart contract code hash, etc. for L2 synchronization.

* **GLOCK** — is a set оf special contracts on GOSH Blockchain.
Aside from managing TIP-3 distributed tokens they also manage the deposits and withdrawals assets of users.
Contract `Checker.sol` receives an external message from `Proposer` with Ethereum blockchain proofs signed by the Ethereum Committee, checks the hash of the blocks lined up in the chain, and deploys the contract `Proposal.sol` that validators check and vote for the Ethereum blocks in GOSH then receives a list of verified transactions and send a message to the root contract `RootTokenContract.cpp`


* **RootTokenContract** - is a smart contract on GOSH that manages user withdrawals. It receives TIP-3 transactions, verifies them and adds transactions to the counter index.
Also it deploys the contract TIP3 wallet contract (`TONTokenWallet.cpp`) and sends wrapped tokens there.

* **TONTokenWallet** - is a custom TIP-3 contract that runs in GOSH Masterchain and in addition to standard functions has `burnTokens` method. It is called when WETH needs to be transferred to Ethereum Blockchain. Burn is proven to ELOCK contract in order to allow for ETH native token withdrawals. 


## **Commission**


### **for deposit to GOSH**


When transferring assets to GOSH, `checker.sol` sends the transfer amount and coefficients `a` and `b` to the `RootTokenContract.cpp` and it calculates the commission amount. Then mints the wrapped tokens to the user TIP3-wallet minus the commission. And the commission is sent to the wallet by the commission in GOSH.


calculated as:

$\frac{a * x}{10 000} + b$

where:

**a**  - commission percentage = 10 (0.1%)

**b** - permanent commission (does not depend on the transfer amount, now = 0)

**х** - amount of tokens to transfer


### **for withdraw to Ethereum**


The commission is calculated in the ELOCK contract.

It consists of 2 parts:

* *Part 1* - the cost of the transaction for the transfer of `WETH` to the recipient

calculated as: 

$ 21000 * gasprice$

where:

**gasprice** - gas price during withdraw transaction

* *Part 2*

calculated as: 

amount of validators' expenses / quantity of transfers to withdraw `WETH` in the current proposal

Then it is sent to the commission wallet.


## **Integration with GOSH L2**


More information about integration with GOSH L2 can be found [here](../integrations/l2.md)


## **Definitions**


**TVM** is a Custom Virtual Machine GOSH Blockchain uses. For the GOSH L2 release we use extended TVM with [additional instructions](overview.md#added-new-tvm-opcodes), thus TVM smart contract can run Signature Verifications and Calculate Hash functions from Ethereum Data.

**Masterchain** is the (-1) work chain of the GOSH blockchain. It is needed for service contracts and validator contracts.

**Shardchain** is shards into which the workchain is split depending on the network load. When it increases, shards split and when they decrease they merge.


**Proposer** is an off-chain program that any user can run on their machine. It packages all necessary data to prove to the GOSH chain that a particular transaction (let’s call them “L2 transactions”) on the Ethereum Network took place and vice versa — to prove to Ethereum ELOCK smart contract (i.e. Ethereum validators) that an L2 transaction took place on the GOSH Blockchain.

Proposer will always accumulate all transactions that are currently not applied to generate the proof, thus ensuring that all transactions of the opposite network are applied. If that is not the case the State Validation function will fail.

**TIP-3** is a distributed token smart contract standard on the GOSH blockchain. It is a formally verified scalable token design for sharded architecture optimized for parallelization.


## Added new TVM opcodes

**KECCAK256** - implements the `keccak256` hashing algorithm for the data provided in the TVM cell

**VERGRTH16** - verify `Groth16 zk-SNARK` proof
