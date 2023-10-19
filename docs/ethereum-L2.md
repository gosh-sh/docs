# **GOSH Ethereum L2**


## **integration with GOSH L2**


### **Introduction**

Endpoint для использования с [Ever-SDK](https://docs.everos.dev/ever-sdk/)

```
сеть main: https://network.gosh.sh
```

Для каждого пользователя при регистрации в GOSH деплоится контракт [**Profile**](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/profile.sol).

Чтобы получить его адрес нужно:

у контракта [**VersionController**](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/gosh/versioncontroller.sol), (1)
{ .annotate }

1.  address (permanent)
    ```
    0:5cbbbce41fc4290f3d4b085ab30912831b710fa2c681f6ea227d4a22f2b304f5
    ```

    ABI можно получить по [ссылке](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/gosh/versioncontroller.abi.json)


вызывать метод:

```
getProfileAddr(string name) returns(address)
```
где:

`name` - имя пользователя

и получаем адрес контракта профиля пользователя.



Затем нужно получить адрес [**SystemContract**](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/gosh/systemcontract.sol) требуемой версии:

для этого в контракте **VersionController** нужно вызвать метод:

```
getVersionAddrMap() returns(SystemContractAddr[])
```

В результате вернется список всех версий контрактов с их адресами:

!!! info
    Сейчас текущая версия 6.1.0: (1)
    { .annotate }

    1.  address systemcontract
        ```
        0:e87874f4a9e46f9f16e0c09c824204836b31d60b16db050a8c7fe329bb43d120
        ```


### **Transfer tokens**


#### * **inside the GOSH network**


Перед переводом на другой GOSH-кошелек нужно проверить задеплоин ли кошелек получателя. для этого нужно вызвать в контракте:
**RootTokenContract** метод [`getWalletAddress`]((ethereum-L2.md#tip3-_1)) указав публичный ключ получателя

Если у получателя TIP3-кошелек не задеплоин, то нужно в контракте TIP3-кошелька `TONTokenWallet`(с которого будет осуществляться перевод) (1)
{ .annotate }

1.  ABI [here](../static/RootTokenContract.abi){:download="TONTokenWallet.abi"}

вызвать метод:

```
void transferToRecipient(
    address_opt answer_addr,
    Tip3Creds   to,
    uint128     tokens,
    uint128     evers,
    uint128     keep_evers,
    bool        deploy,
    uint128     return_ownership,
    opt<cell>   notify_payload
  )
```

В результате для получателя будет задеплоин пустой TIP3-кошелек.


<!-- 
`await this.run('transferToRecipient', {
  _answer_id: 0,
  answer_addr: null,
  to: { pubkey, owner: null },
  tokens: 0,
  evers: BigInt(4.5 * 10 ** 9).toString(),
  keep_evers: BigInt(4 * 10 ** 9).toString(),
  deploy: true,
  return_ownership: 0,
  notify_payload: null,
})` -->

Затем, для перевода TIP3-токенов пользователю, нужно  
в контракте **TONTokenWallet**  
вызвать метод:

```
void transfer(
    address_opt answer_addr,
    address     to,
    uint128     tokens,
    uint128     evers,
    uint128     return_ownership,
    opt<cell>   notify_payload
)
```
where:  
    `answer_addr`      - (опциональный) Answer address (should be `null`)  
    `to`               - Destination TIP3 wallet address  
    `tokens`           - Amount of tokens to transfer  
    `evers`            - Native funds to process. For internal requests, this value is ignored and processing costs will be taken from attached value  
    `return_ownership` - Return ownership - to decrease lend ownership provided for the caller contract (additionally) (should be `0`)  
    `notify_payload`   - Payload (arbitrary cell) - if specified, will be transmitted into dest owner's notification (should be `null`)  

<!-- 
`await this.run('transfer', {
  _answer_id: 0,
  answer_addr: null,
  to: address,
  tokens: amount.toString(),
  evers: BigInt(4 * 10 ** 9).toString(),
  return_ownership: 0,
  notify_payload: null,
})` -->

#### * **from Etherium to GOSH**

Для перевода ETH в GOSH необходимо  
в контракте **ELock** (1)
{ .annotate }

1.  is a GOSH L2 smart contract on Ethereum Blockchain.
    It receives deposits from users, manage withdrawals and locks user funds. ELOCK is also counting its total balance, total transaction count and stores root Merkle proofs, withdrawal smart contract code hash, etc. for L2 synchronization.
    
    address in Etherium:
    ```
    0x135d03AF576633B0C99FB9F0A0c6Aa9cE8D3C67E
    ```

    ABI [here](../static/Elock.json){:download="Elock.json"}

вызвать метод with attach value, количество ETH, которые будут переведены в GOSH:

```
deposit(uint256 pubkey) public payable
```

где,  

`pubkey` - публичный ключ получателя в GOSH  

Затем необходимо [вычислить адрес TIP3-кошелька пользователя](ethereum-L2.md#tip3-_1) в GOSH и ожидать перевода токенов (`WETH` - wrapped `ETH`) на полученный адрес.

!!! exsample annotate "example of calling an ELock contract in Etherium"

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


#### * **from GOSH to Etherium**


Для перевода `WETH` в Etherium необходимо  
в контракте **TONTokenWallet** пользователя  
вызвать метод:

```
void burnTokens(uint128 tokens, uint256 to)
```
где:  
`tokens` - количество WETH, которые будут переведены в Etherium  
`to`- адрес кошелька получателя в Etherium

Затем ожидать поступления ETH на кошелек получателя в Etherium.



### Getting the TIP3-wallet address by user name


Зная адрес контракта **профиля** пользователя (1)
{ .annotate }

1.  ABI можно получить по [ссылке](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/profile.abi.json)

вызываем в нем метод:

```
getAccess() returns(mapping(uint256 => uint8))
```

получаем список всех публичных ключей пользователя

!!! warning annotate "Important"
    Из списка необходимо брать нулевой ключ

Затем по публичному ключу можно будет определить [адрес TIP3-кошелька пользователя](ethereum-L2.md#tip3-_1).


### **Getting the user's TIP3-wallet address using the user's public key**


Для этого в контракте **RootTokenContract** (1)
{ .annotate }

1.  address
    ```
    0:1792014440934b9c4024c97221b49c50bd2e2db1426b612ba4c6694b144f5e77
    ```

    ABI [here](../static/RootTokenContract.abi){:download="RootTokenContract.abi"}

вызываем метод:

```
address getWalletAddress(uint256 pubkey, address_opt owner)
```

где:  
`pubkey` - публичный ключ пользователя  
`owner` - опциональный параметр, не используется



### **Getting a list of incoming messages of the contract**


!!! note annotate "пример получения сообщений аккаунта:"
    https://github.com/gosh-sh/gosh/blob/dev/web/src/blockchain/contract.ts#L90

!!! info
    Использование пагинации в SDK
    https://docs.everplatform.dev/samples/graphql-samples/accounts#pagination-parameters


### **Get info about TIP3-wallet details**


Для получения информации о кошельке:  
в контракте **TONTokenWallet**

вызывается метод:

```
details_info getDetails()
```

и получаем структуру данных:

```
struct details_info {
  string            name;              ///< Token name.
  string            symbol;            ///< Token short symbol.
  uint8             decimals;          ///< Decimals for ui purposes. ex: balance 100 with decimals 2 will be printed as 1.00.
  uint128           balance;           ///< Token balance of the wallet.
  uint128           locked;            ///< Locked token balance of the wallet.
  uint256           root_pubkey;       ///< Public key of the related RootTokenContract.
  address           root_address;      ///< Address of the related RootTokenContract.
  uint256           wallet_pubkey;     ///< Public key of wallet owner (User id for FlexWallet).
  address_opt       owner_address;     ///< Owner contract address for internal ownership, will be 0:0..0 otherwise.
  opt<uint256>      lend_pubkey;       ///< Lend ownership pubkey.
  lend_owners_array lend_owners;       ///< All lend ownership records of the contract.
  uint128           lend_balance;      ///< Summarized lend balance to all targets.
                                       ///< Actual active balance will be `balance - lend_balance`.
  opt<bind_info>    binding;           ///< Flex binding info.
  uint256           code_hash;         ///< TIP3 wallet code hash to verify other wallets.
  uint16            code_depth;        ///< TIP3 wallet code depth to verify other wallets.
  int8              workchain_id;      ///< Workchain id.
}
```


<!-- В каждом ДАО, в котором пользователь является членом, у него может быть до 64 кошельков.
Кошелек с индексом 0 - основной, остальные - дополнительные.

Чтобы получить адрес кошелька пользователя в конкретном ДАО у `systemcontract`

abi: https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.1.0/contracts/gosh/systemcontract.abi.json

вызывается  метод 
`getAddrWallet(address pubaddr, address dao, uint128 index) returns(address)`,
где 
pubaddr - адрес контракта профиля пользователя,
dao - адрес контракта ДАО
index - индекс кошелька (0 - основной, 1-64 - дополнительные) -->