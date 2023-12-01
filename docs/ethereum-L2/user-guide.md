# **User Guide**


Any DAO on GOSH can become Ethereum Layer 2 with a click of a button.

!!! info
    This is only possible in the GOSH version of at least 6.1.0

## Deposit ETH to GOSH

To make a transfer between wallets, go to the **Ethereum** tab:

![](../images/ethereum_usage_begin2.jpg)

or select this section by clicking on your profile in the right corner:

![](../images/ethereum_usage_begin1.jpg)

Now we can test the ETH transfer in the alpha version.


Click on:

![](../images/ethereum_usage_begin3.jpg)

the "Cross-chain transfer" page will open for you.


In the **Accounts** section, click **Connect** to log into a software cryptocurrency wallet **MetaMask**

![](../images/ethereum_usage_connect.jpg)

Enter the amount you want to send

!!! note
    The amount must be greater than or equal to 0.01


!!! warning
    The contract has not been formally verified yet. Please do not send a lot!

![](../images/ethereum_usage_from.jpg)

Enter the wallet address or GOSH username of the recipient for the transfer.
The **Amount** field will indicate the transferred amount (minus the commission) that will be credited to the recipient's wallet in GOSH.

![](../images/ethereum_usage_to.jpg)

After depositing the GOSH contract on Ethereum, you will receive the corresponding amount of WITH tokens (Wrapper Ethereum tokens) in your GOSH network wallet.

![](../images/ethereum_usage_transfer_comleted.jpg)


## Withdraw WETH to Ethereum

To withdraw tokens from GOSH to Ethereum, go to the **Ethereum** tab on the DAO page

![](../images/ethereum_usage_begin2.jpg)

or select this section by clicking on your profile in the right corner:

![](../images/ethereum_usage_begin1.jpg)

the "Cross-chain transfer" page will open for you:

![](../images/ethereum_usage_withdraw_page_cross_chain_tr.jpg)

In the **Accounts** section, click **Connect** to log into a software cryptocurrency wallet **MetaMask**

![](../images/ethereum_usage_withdraw_connect_metamask.jpg)

!!! info

    In the future, the balances of your wallets on GOSH and Ethereum will be displayed here


In the **From** section, select the **GOSH** blockchain and enter the sender's wallet address or GOSH username along with the amount of WETH tokens you wish to withdraw:

![](../images/ethereum_usage_withdraw_from.jpg)


In the **To**section, make sure to choose the **Ethereum** blockchain network and verify the Receiver's wallet address for accuracy before proceeding. The `ETH` amount will be automatically calculated.

![](../images/ethereum_usage_withdraw_to.jpg)

Please click on the **Next** button to proceed.

On the right, in the **Summary** section, you can see information about the amount of assets received and sent.

![](../images/ethereum_usage_withdraw_sammary.jpg)

The amount of the expected commission for the transfer and and the time before the withdrawal of assets is also indicated


!!! info

    Tokens are withdrawn every 3 hours

<!-- TODO description

![](../images/ethereum_usage_withdraw_step2_transf.jpg)-->

Please wait until the process of sending `WETH` tokens and receiving `ETH` fully completed

![](../images/ethereum_usage_withdraw_step3_compl.jpg)





## Deposit ERC20 to GOSH

To make a transfer `ERC20` tokens, go to the **Ethereum** tab:

![](../images/ethereum_usage_begin2.jpg)

or select this section by clicking on your profile in the right corner:

![](../images/ethereum_usage_begin1.jpg)

Click on:

![](../images/ethereum_usage_begin3.jpg)

the **Cross-chain transfer** page will open for you.

Let's look at the token transfer using the example of the USDC.

In the **From** section, select the token to transfer to GOSH

![](../images/ethereum_usage_transfer_usdc-to-gosh_1_from.jpg)

To log into a software cryptocurrency wallet **MetaMask**, you can either click on **Connect wallet** or go to the **Accounts** section and click on **Connect**.

![](../images/ethereum_usage_transfer_usdc-to-gosh_2_accounts.jpg)

Enter the amount you want to send

!!! note
    The amount must be greater than or equal to 0.011


![](../images/ethereum_usage_transfer_usdc-to-gosh_3_from_sum.jpg)

Enter the wallet address or GOSH username of the recipient for the transfer.

The **Amount** field will indicate the transferred amount (minus the commission) that will be credited to the recipient's wallet in GOSH.

The Summary section will display detailed information about the transfer

![](../images/ethereum_usage_transfer_usdc-to-gosh_4_to.jpg)


![](../images/ethereum_usage_transfer_usdc-to-gosh_5_summary.jpg)

And click **Next** button

The transfer process has three sub-steps.  
The first one is to approve tokens, followed by deposit tokens, and finally, waiting for the transfer to be completed.  

Once you click on the **`Approve`** button, you'll be authorizing the ELOCK contract to initiate the transfer of the specified amount. 

![](../images/ethereum_usage_transfer_usdc-to-gosh_6_aprove_tokems.jpg)


In the opened **MetaMask** window, confirm the necessary parameters for the transfer.

![](../images/ethereum_usage_transfer_usdc-to-gosh_7_spending_cap.jpg)

![](../images/ethereum_usage_transfer_usdc-to-gosh_8_approve.jpg)




Click on the **Deposit** button and then check and confirm the transfer parameters in your **MetaMask** wallet. 

![](../images/ethereum_usage_transfer_usdc-to-gosh_9_deposit_tokens_elock.jpg)

It's important to ensure that the transfer is being made to the **ELOCK** contract at this step.

!!! info annotate "**address of the ELOCK contract in Ethereum:**"

    ```
    0x54a858bBD5968Eb755e54C45a3fe5B002bE3c254
    ```


![](../images/ethereum_usage_transfer_usdc-to-gosh_10_confirm.jpg)



After that, you just need to wait for the transfer to be completed.

![](../images/ethereum_usage_transfer_usdc-to-gosh_11_receive_tokens.jpg)

After successful completion of the transfer, you will see a confirmation:

![](../images/ethereum_usage_transfer_usdc-to-gosh_12_completed.jpg)


If you want to view your asset balance, you can find it in the **Accounts** section. To do this select the relevant token in the "From" tab.

![](../images/ethereum_usage_balance_1.jpg)
![](../images/ethereum_usage_balance_2.jpg)




## Withdraw ERC20 to Ethereum

<!-- DAO members can choose to have their token available in Ethereum, effectively making any project its own L2. And because GOSH L2 supports ERC-20 Tokenization, we offer easy ecosystem integration for any project. -->

To withdraw ERC20 tokens from GOSH to Ethereum, go to the **Ethereum** tab on the DAO page
and log into a software cryptocurrency wallet **MetaMask**

![](../images/ethereum_usage_withdraw_usdc_1_connection_metamask.jpg)

In the **From** section, select the asset that you want to withdraw to Ethereum

![](../images/ethereum_usage_withdraw_usdc_1-2_usdc-gosh.jpg)

The available assets will be displayed in the **Accounts** section

![](../images/ethereum_usage_withdraw_usdc_2_accounts.jpg)

Enter the desired number of tokens to withdraw

![](../images/ethereum_usage_withdraw_usdc_3_from.jpg)

The Summary section will display detailed information about the withdraw

!!! info

    Tokens are withdrawn every 3 hours

![](../images/ethereum_usage_withdraw_usdc_4_summury.jpg)

In the **To** section, in the **Recipient** field, you must specify the recipient's Ethereum wallet address.  
The number of tokens will be calculated automatically.

Please click on the Next button to proceed.

![](../images/ethereum_usage_withdraw_usdc_5_to.jpg)


The transfer of the ERC20 tokens from GOSH to Ethereum will take some time.

<!-- ![](../images/ethereum_usage_withdraw_step3_compl.jpg) -->

After the transfer process, you will be able to view the list of your assets that have been transferred from GOSH to Ethereum in the **Your pending withdrawals** section.  
These assets are now located in Ethereum on the balance **ELOCK** contract, and you can withdraw them to your wallets by clicking on the **Withdraw** button.

![](../images/ethereum_usage_withdraw_usdc_6_pending.jpg)

Confirm the withdrawal of tokens to your wallet

![](../images/ethereum_usage_withdraw_usdc_7_metamask_confirm.jpg)

Wait for the tokens to arrive on the balance of your Ethereum wallet

<!-- ![](../images/ethereum_usage_withdraw_usdc_8_no_pending.jpg) -->

![](../images/ethereum_usage_withdraw_usdc_9_accounts_after_withdraw.jpg)