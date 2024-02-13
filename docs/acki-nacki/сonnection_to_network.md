## **Mainnet**




## **Testnet**

Endpoint of [testnet](https://ackinacki-testnet.tvmlabs.dev)


To explore the Aсki Naсki blockchain, you can use the [Aсki Naсki explorer](https://ackinacki-testnet.tvmlabs.dev/landing){:target="_blank"}  


### SDK

<!-- TODO after release tvm-labs-->
<!-- https://github.com/tvmlabs/tvm-sdk -->

current sdk version: https://github.com/gosh-sh/ever-sdk/tree/feature/masterchain-free

More information can be found [here](https://docs.everos.dev/ever-sdk/)


### tonos-cli

current version:

https://github.com/gosh-sh/tonos-cli/tree/feature/remove_localhost_resolve



### GraphQL playground

<!-- TODO after release tvm-labs-->
<!-- https://github.com/tonlabs/ever-cli -->

https://ackinacki-testnet.tvmlabs.dev/graphql


### test tokens

To test your developments online, you will need tokens. To receive them, please contact us: 
[Channel on Telegram](https://t.me/+1tWNH2okaPthMWU0)


<!-- TODO 
change the address when a non-SE-giver is created -->

<!-- Giver

In Acki Nacki the **giver** is pre deployed at 0:ece57bcc6c530283becbbd8a3b24d3c5987cdddc3c8b7b33be6e4a6312490415 address.

**Usage**

Method: [**`sendTransaction`**](contracts.md#sendtransaction)

PARAMETERS:  

* **`dest`** [address] - destination address;
{ .ml-params }
* **`value`** [uint128]- amount to send, in nanotokens;
{ .ml-params }
* **`bounce`** [bool]- bounce flag of the message;
{ .ml-params }


**Abi:**

```
{"ABI version": 2,
    "header": ["time", "expire"],
    "functions": [
        {
            "name": "upgrade",
            "inputs": [
                {"name":"newcode","type":"cell"}
            ],
            "outputs": [
            ]
        },
        {
            "name": "sendTransaction",
            "inputs": [
                {"name":"dest","type":"address"},
                {"name":"value","type":"uint128"},
                {"name":"bounce","type":"bool"}
            ],
            "outputs": [
            ]
        },
        {
            "name": "getMessages",
            "inputs": [
            ],
            "outputs": [
                {"components":[{"name":"hash","type":"uint256"},{"name":"expireAt","type":"uint64"}],"name":"messages","type":"tuple[]"}
            ]
        },
        {
            "name": "constructor",
            "inputs": [
            ],
            "outputs": [
            ]
        }
    ],
    "events": [
    ]
}
```

**Using tonos-cli:**

```
./tonos-cli -u https://ackinacki-testnet.tvmlabs.dev/ call 0:ece57bcc6c530283becbbd8a3b24d3c5987cdddc3c8b7b33be6e4a6312490415 sendTransaction "{\"dest\":\"0:175a09397d7feab71ff152aa162292ee289424d924f1558ab3bc5b1f963795fc\", \"value\":10000000000, \"bounce\":false}" --abi ../../../segiver/GiverV2.abi.json --sign ../../../segiver/seGiver.keys.json
```

 -->
