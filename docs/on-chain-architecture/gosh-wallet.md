# GOSH Wallet

The GOSH blockchain is a system of interconnected smart contracts. Every repository, every file and commit are smart contracts, where data is written to the blockchain.

Writing data to the blockchain requires cryptographic signatures and fees.

For this reason every GOSH user needs to have a wallet and a pair of cryptographic keys. 

Every operation on GOSH is carried out by user wallets.

!!! info
    GOSH wallets are written with the express purpose of facilitating open-source development.

    Fees on GOSH are not paid to Validators but are instead transferred to the Free Software Giver — Which funds the GOSH Free Service Area  — these fees are used to replenish the Special User Wallet contracts to automatically pay for gas fees of other contracts in the Free Service Area.

    These contracts can only transfer tokens between other contracts within the Area and are not transferable outside, meaning they are pure Utility Tokens. These tokens are SHELL coins, here used as a Unit of Account for Payment Gateways.

    **So in effect this means any developer can use the GOSH blockchain for free, without paying any gas, and sell their services using Fiat Payment Gateways without a need to KYC/AML.** This payment Gateway is built into GOSH.


There are two types of wallets GOSH users can deploy:

* __A DAO Member Wallet__, which is deployed to a GOSH user after they become a member of a DAO. This wallet stores both voting and non-voting tokens

* __A Limited Wallet__ (for non-DAO members), which is deployed to a GOSH user when they view any DAO or if non-voting tokens of any DAO were transferred to them.

    A user with a Limited Wallet in the DAO can:

    - [create a proposal to add yourself to the DAO](../working-with-gosh/gosh-web.md#request-dao-membership) (if it [is allowed in the dao](../working-with-gosh/gosh-web.md#dao-set-up));

    - can be assigned as a reviewer to the [Task](../working-with-gosh/gosh-web.md#working-with-task);

    - can create a proposal on PR (coming soon).

!!! info
    For a DAO member, not one wallet is deployed, but a whole system of 64 wallet contracts. This allows for parallelization when sending external messages.

Refer to [GOSH Web](../working-with-gosh/gosh-web.md) or [Docker Extension](../working-with-gosh/docker-extension.md) sections to find out how to create your account and get started with GOSH.

