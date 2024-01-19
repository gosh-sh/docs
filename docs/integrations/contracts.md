
# **Contracts**

<!-- on-chain-architecture/gosh-smart-contracts/ -->

## **Profile**
**this contract is deployed for each user when registering with GOSH. It stores the user's name and its public keys.**
{ .ml-params }

[[source code]](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profile.sol){:target="_blank"}
{ .ml-params }

[[ABI]](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profile.abi.json){:target="_blank"}
{ .ml-params }



<a id="getaccess" href="https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profile.sol#L352">**getAccess**</a>() returns(mapping(uint256 => uint8))


RETURNS:  

the list of all the user's public keys with their numbers.  
It is necessary **to take the zeroth pubkey** from the list
{ .ml-params }

<!-- RETURN TYPE  

*mapping(uint256 => uint8)*
{ .ml-params } -->




## **VersionController**  
**a contract version manager used when upgrading GOSH smart contracts**
{ .ml-params }

[[source code]](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/versioncontroller.sol){:target="_blank"}
{ .ml-params }

[[ABI]](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/versioncontroller.abi.json){:target="_blank"}
{ .ml-params }

!!! info
    **address (permanent):**  

    ```
    0:5cbbbce41fc4290f3d4b085ab30912831b710fa2c681f6ea227d4a22f2b304f5
    ```



<a id="getprofileaddr" href="https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/versioncontroller.sol#L224">**getProfileAddr**</a>(string name) returns(address)


***The function for getting the address of the user's **Profile*****
{ .ml-params }

PARAMETERS:  


* **`name`** (*string*) - user's name
{ .ml-params }

RETURNS:  

the address of the user's **Profile** contract
{ .ml-params }

<!-- RETURN TYPE

*address*
{ .ml-params } -->




<!-- ethereum-L2/overview/#contracts -->

## **ELOCK**
**is a GOSH L2 smart contract on Ethereum Blockchain. It receives deposits from users, manages withdrawals, and locks user funds. **ELOCK** also counts its total balance, and total transaction count and stores root Merkle proofs, withdrawal smart contract code hash, etc. for L2 synchronization.**

<!-- [[source code]]() -->


[[ABI]](../static/Elock.json){:download="Elock.json"}
{ .ml-params }

!!! info
    **address in Ethereum:**  

    ```
    0x54a858bBD5968Eb755e54C45a3fe5B002bE3c254
    ```



<a id="deposit" href="">**deposit**</a>(uint256 pubkey)  

***Allows a user to deposit `Ether` (transfered as value) into the Elock-contract for locking in it.***
The corresponding amount of wrapped tokens (`WETH`) in GOSH will be minted for the amount of the
blocked funds.  
{ .ml-params }

PARAMETERS:  

* **`pubkey`**  (*uint256*) - the recipient's public key in GOSH. Used to derive the address of the
user's token wallet for minting wrapped tokens to it.  
{ .ml-params }


!!! example annotate "example of calling the ELock contract in Ethereum"

    ``` cpp
    const elock = new data.web3.instance.eth.Contract(
        ELockAbi.abi,
        AppConfig.elockaddr,
    )

    const edata = elock.methods.deposit(data.summary.to.user.value.pubkey).encodeABI()
            
    const receipt = await data.web3.instance.eth.sendTransaction({
        from: data.web3.address,
        to: AppConfig.elockaddr,
        value: data.web3.instance.utils.toWei(data.summary.from.amount, 'ether'),
        data: edata,
        gasLimit: 100000,
        maxPriorityFeePerGas: 25000,
    })
    ```



<a id="depositerc20" href="">**depositERC20**</a>(address token, uint256 value, uint256 pubkey)  

***Allows a user to deposit ERC20 tokens into the Elock-contract for locking in it.  The corresponding amount of wrapped tokens in GOSH will be minted for the amount of the blocked funds.***  
Before calling deposit, the specified number of tokens must be available for transfer for the Elock
address.
{ .ml-params }


PARAMETERS:  

* **`token`** (*address*) - address of the ERC20 token contract.  
* **`value`** (*uint256*) - deposited number of tokens.  
* **`pubkey`** (*uint256*) - the recipient's public key in GOSH. Used to derive the address of the
user's token wallet for minting wrapped tokens to it.  
{ .ml-params }






<a id="withdrawerc20" href="">**withdrawERC20**</a>(address token)  

***Requests the withdrawal of the specified tokens for the caller (`msg.sender`).***  
Tokens must be approved for withdrawal. The commission must be attached to the function call.
{ .ml-params }

PARAMETERS:  

* **`token`** (*address*) - address of the ERC20 token contract.  
{ .ml-params }



<a id="geterc20approvement" href="">**getERC20Approvement**</a>(address token, address recipient) returns (uint value, uint commission)  

***For the specified token and recipient, it returns the number of tokens available for withdrawal (withdrawERC20) and the commission to be transferred for the withdrawal function.***
{ .ml-params }

PARAMETERS:  

* **`token`** (*address*) - address of the ERC20 token contract.  
* **`recipient`** (*address*) - the address of the recipient of the withdrawn tokens 
{ .ml-params }


RETURNS:  

**value** (*uint256*) - the number of tokens approved for withdrawal.  
**commission** (*uint256*) - the amount of commission for withdrawal.  
{ .ml-params }




<!-- <a id="gettokenroots" href="">**getTokenRoots**</a>() returns(address) -->

<a id="gettokenroots" href="">**getTokenRoots**</a>() returns (address[] memory roots)

***The function returns an array of addresses where each address represents a supported ERC20 token in GOSH Ethereum L2.***  
{ .ml-params }

RETURNS:  

**roots** (*address[]*) - list of addresses of ERС20 tokens  
{ .ml-params }






## **GLOCK**  
**is a set оf special contracts on GOSH Blockchain.**  
Aside from managing TIP-3 distributed tokens they also manage the deposits and withdrawals assets of users.  
Contract **`Checker.sol`** receives an external message from [**`Proposer`**](../ethereum-L2/overview.md#definitions " is an off-chain program which packages all necessary data to prove to GOSH chain that a particular transaction (let’s call them “L2 transactions”) on Ethereum Network took place and vise versa — to prove to Ethereum ELOCK smart contract (i.e. Ethereum validators) that an L2 transaction took place on the GOSH Blockchain") with Ethereum blockchain proofs signed by the Ethereum Committee, checks the hash of the blocks lined up in the chain, and deploys the contract **`Proposal.sol`** that validators check and vote for the Ethereum blocks in GOSH then receives a list of verified transactions and send a message to the root contract **`RootTokenContract.cpp`**
{ .ml-params }

### **Checker**


<!-- [[source code]]() -->

[[ABI]](../static/checker.abi.json){:download="checker.abi.json"}
{ .ml-params }

!!! info
    **address in GOSH:**  

    ```
    0:17eb654c5fca0027d47a4564139df71bec46b2277d71f6674ecd9dc55e52fb78
    ```


<a id="getRootAddr" href="">**getRootAddr**</a>(RootData data) returns(address)

***The function returns TIP-3 root contract address***
{ .ml-params }

PARAMETERS

* **`RootData.name`**     (*string*) - ERC20 token name;  
* **`RootData.symbol`**   (*string*) - ERC20 token symbol;  
* **`RootData.decimals`** (*uint8*)  - ERC20 token decimals;  
* **`RootData.ethroot`**  (*uint256*)- ERC20 token address;  
{ .ml-params }


RETURNS

address TIP-3 root for wrapped ERС20 token in GOSH 
{ .ml-params }



<!-- ### **Proposal.sol**

[[source code]]()

[[ABI]]()

PARAMETERS
RETURNS
RETURN TYPE  -->






## **RootTokenContract**  
**is a smart contract on GOSH that manages user withdrawals. It receives TIP-3 transactions, verifies them and adds transactions to the counter index.**  
**Also it deploys the TIP-3 wallet contract (`TONTokenWallet.cpp`) and sends wrapped tokens there.**
{ .ml-params }

<!-- [[source code]]() -->

[[ABI]](../static/RootTokenContract.abi){:download="RootTokenContract.abi"}
{ .ml-params }


!!! info
    **address for TIP-3 token `ETH`:**

    ```
    0:d6182377a82e7f159f1b9995b2582ac933791599a4da9d72cc2c7812f056592d
    ```  



<a id="getwalletaddress" href="">**getWalletAddress**</a>(uint256 pubkey, address_opt owner)  

***The function for getting the user's TIP-3 wallet address***
{ .ml-params }


PARAMETERS:  

* **`pubkey`** - user's public key
{ .ml-params }
* **`owner`** - optional parameter, not used
{ .ml-params }

RETURNS:  

user's wallet address
{ .ml-params }

<!-- RETURN TYPE -->


## **TONTokenWallet**  

**is a custom TIP-3 contract that runs in GOSH Masterchain. Allows to manage TIP-3 tokens and transfers it to Ethereum for withdrawal**
{ .ml-params }

<!-- [[source code]]() -->

[[ABI]](../static/TONTokenWallet.abi){:download="TONTokenWallet.abi"}
{ .ml-params }


<a id="transfertorecipient" href="">**transferToRecipient**</a>(  
    address_opt answer_addr,  
    Tip3Creds   to,  
    uint128     tokens,  
    uint128     evers,  
    uint128     keep_evers,  
    bool        deploy,  
    uint128     return_ownership,  
    opt<cell>   notify_payload  
)

***The function for deploying empty TIP-3 wallet to another user***
{ .ml-params }

PARAMETERS:  

* **`answer_addr`** - Answer address, **(should be `null`)**  
* **`to`** - Recipient credentials (pubkey + owner **(should be `null`)**)  
* **`tokens`** - Amount of tokens to transfer, **(should be `0`)**  
* **`evers`** - Native funds to process. For internal requests, this value is ignored and processing costs will be taken from attached value  
* **`keep_evers`** - Evers to keep in destination wallet  
* **`deploy`** - **(should be `true`)** then the contract will send acceptTransfer message with StateInit to also deploy new TIP-3 wallet (if it doesn't already exist) with the provided recipient public key and recipient internal owner  
* **`return_ownership`** - Return ownership - to decrease lend ownership for the caller contract (additionally), **(should be `0`)**  
* **`notify_payload`** - (optional) < Payload (arbitrary cell) - if specified, will be transmitted into dest owner's notification, **(should be `0`)**  

<!-- RETURNS
RETURN TYPE -->


<a id="transfer" href="">**transfer**</a>(  
    address_opt answer_addr,  
    address     to,  
    uint128     tokens,  
    uint128     evers,  
    uint128     return_ownership,  
    opt<cell>   notify_payload  
)  

***The function transfers the TIP3-tokens between TIP-3 user wallets.***
{ .ml-params }

PARAMETERS:  

* **`answer_addr`**      - (optional) Answer address **(should be `null`)**  
* **`to`**               - Destination TIP-3 wallet address  
* **`tokens`**           - Amount of tokens to transfer  
* **`evers`**            - Native funds to process. For internal requests, this value is ignored and processing costs will be taken from attached value  
* **`return_ownership`** - Return ownership - to decrease lend ownership provided for the caller contract (additionally) **(should be `0`)**  
* **`notify_payload`**   - Payload (arbitrary cell) - if specified, will be transmitted into dest owner's notification **(should be `null`)**  
{ .ml-params }




<a id="burntokens" href="">**burnTokens**</a>(uint128 tokens, uint256 to)

***The function burns tokens for transfer to Ethereum***  
{ .ml-params }

<!-- Then it remains to wait for the transfer of `ETH` to the recipient's wallet in Ethereum. -->
PARAMETERS:  

* **`tokens`** - amount WETH, which will be transferred to Ethereum  
* **`to`** - the address of the recipient's wallet in Ethereum
{ .ml-params }




<a id="getdetails" href="">**getDetails**</a>()

***The function returns information about the TIP-3 wallet***
{ .ml-params }


RETURNS:  

the data structure:
{ .ml-params }


```
struct details_info {
  string            name;           // Token name.
  string            symbol;         // Token short symbol.
  uint8             decimals;       // Decimals for ui purposes. ex: balance 100 with decimals 2 will be printed as 1.00.
  uint128           balance;        // Token balance of the wallet.
  uint128           locked;         // Locked token balance of the wallet.
  uint256           root_pubkey;    // Public key of the related RootTokenContract.
  address           root_address;   // Address of the related RootTokenContract.
  uint256           wallet_pubkey;  // Public key of wallet owner (User id for FlexWallet).
  address_opt       owner_address;  // Owner contract address for internal ownership, will be 0:0..0 otherwise.
  opt<uint256>      lend_pubkey;    // Lend ownership pubkey.
  lend_owners_array lend_owners;    // All lend ownership records of the contract.
  uint128           lend_balance;   // Summarized lend balance to all targets.
                                    // Actual active balance will be `balance - lend_balance`.
  opt<bind_info>    binding;        // Flex binding info.
  uint256           code_hash;      // TIP-3 wallet code hash to verify other wallets.
  uint16            code_depth;     // TIP-3 wallet code depth to verify other wallets.
  int8              workchain_id;   // Workchain id.
}
```


## **Giver for Acki Nacki test network**  

**This is a giver for receiving test tokens on the https://ackinacki-testnet.tvmlabs.dev/**
{ .ml-params }

<!-- [[source code]]() -->

[[ABI]](../static/TONTokenWallet.abi){:download="TONTokenWallet.abi"}
{ .ml-params }


<a id="transfertorecipient" href="">**transferToRecipient**</a>(  
    address_opt answer_addr,  
    Tip3Creds   to,  
    uint128     tokens,  
    uint128     evers,  
    uint128     keep_evers,  
    bool        deploy,  
    uint128     return_ownership,  
    opt<cell>   notify_payload  
)

***The function for deploying empty TIP-3 wallet to another user***
{ .ml-params }

PARAMETERS:  

* **`answer_addr`** - Answer address, **(should be `null`)**  
* **`to`** - Recipient credentials (pubkey + owner **(should be `null`)**)  
* **`tokens`** - Amount of tokens to transfer, **(should be `0`)**  
* **`evers`** - Native funds to process. For internal requests, this value is ignored and processing costs will be taken from attached value  
* **`keep_evers`** - Evers to keep in destination wallet  
* **`deploy`** - **(should be `true`)** then the contract will send acceptTransfer message with StateInit to also deploy new TIP-3 wallet (if it doesn't already exist) with the provided recipient public key and recipient internal owner  
* **`return_ownership`** - Return ownership - to decrease lend ownership for the caller contract (additionally), **(should be `0`)**  
* **`notify_payload`** - (optional) < Payload (arbitrary cell) - if specified, will be transmitted into dest owner's notification, **(should be `0`)**  
sendTransaction




