
## __Proposals and voting in SMV (Soft Majority Vote)__

The main mechanism of interaction in the DAO is voting. Any action in a DAO requires a vote and is created through Proposals, and a [**soft-majority vote (SMV)**](../../on-chain-architecture/organizations-gosh-dao-and-smv.md#soft-majority-voting) of all other DAO members may be required to approve it. 

<!-- Branches could be locked to require any changes to them to be voted on by DAO SMV. -->

<!-- Actions that require a DAO vote are performed by creating a proposal. -->

!!! warning
    To create an proposal, you must have at least 20 tokens on your wallet balance.

## __Types of Proposals:__

* [**Create a pull request**](../gosh-web/repository.md#create-pull-request)
* **Add branch protection**
* **Remove branch protection**
* [**Add DAO member**](../gosh-web/members.md#adding-members-to-dao)
* [**Remove DAO member**](../gosh-web/members.md#delete-members-from-the-dao)
* [**Upgrade DAO**](../gosh-web/dao-set-up.md#upgrade)
* [**Create task**](../gosh-web/task.md#create-task)
* [**Delete task**](../gosh-web/task.md#deletе-task)
* [**Create repository**](../gosh-web/repository.md#create-repository)
* **Add voting tokens**
* **Add regular tokens**
* **Mint DAO tokens**
<!-- * **Add DAO tag**
* **Remove DAO tag** -->
* **Disable minting DAO tokens**
* **Change DAO member Karma**

<!-- !!! Warning
    Be careful when distributing karma among the members of the TAO.
    Avoid the possibility of a preponderance in the votes of one of the DAO members.
    To avoid a situation where one participant will be able to transfer the entire balance of the DAO to his wallet. -->


* **Multi proposal** - includes several offers at once. 

    For example: [providing the membership to the DAO by the member of the DAO](../gosh-web/members.md#adding-members-to-dao)


<!-- * **Add repository tag**
* **Remove repository tag**
* **Update repository description** -->
* **Allow event discussions**
* **Show event progress**
<!-- * **Upgrade repository tags** -->
* [**Ask DAO membership allowance**](../gosh-web/members.md#request-dao-membership)

<!-- 

status:
In progress
Accepted
Rejected


TODO 
kinds of proposals:
1: 'Pull request',  // SETCOMMIT_PROPOSAL_KIND = 1
2: 'Add branch protection',   //ADD_PROTECTED_BRANCH_PROPOSAL_KIND = 2
3: 'Remove branch protection',   //DELETE_PROTECTED_BRANCH_PROPOSAL_KIND = 3
                                 //SET_TOMBSTONE_PROPOSAL_KIND = 4
5: 'Add DAO member',    //DEPLOY_WALLET_DAO_PROPOSAL_KIND = 5
6: 'Remove DAO member',   //DELETE_WALLET_DAO_PROPOSAL_KIND = 6
7: 'Upgrade DAO',     //SET_UPGRADE_PROPOSAL_KIND = 7
//8: 'Change DAO config',
//9: 'Confirm task',
10: 'Delete task',    //TASK_DESTROY_PROPOSAL_KIND = 10
11: 'Create task',    //TASK_DEPLOY_PROPOSAL_KIND = 11
12: 'Create repository',  //DEPLOY_REPO_PROPOSAL_KIND = 12
13: 'Add voting tokens',  //ADD_VOTE_TOKEN_PROPOSAL_KIND = 13
14: 'Add regular tokens', //ADD_REGULAR_TOKEN_PROPOSAL_KIND = 14
15: 'Mint DAO tokens',   //MINT_TOKEN_PROPOSAL_KIND = 15
16: 'Add DAO tag',     //DAOTAG_PROPOSAL_KIND = 16
17: 'Remove DAO tag',  //DAOTAG_DESTROY_PROPOSAL_KIND = 17
18: 'Disable minting DAO tokens',  //ALLOW_MINT_PROPOSAL_KIND = 18
19: 'Change DAO member allowance', //CHANGE_ALLOWANCE_PROPOSAL_KIND = 19
20: 'Multi proposal',  //MULTI_PROPOSAL_KIND = 20
21: 'Add repository tag',  //REPOTAG_PROPOSAL_KIND = 21
22: 'Remove repository tag', //REPOTAG_DESTROY_PROPOSAL_KIND = 22
23: 'Update repository description', //CHANGE_DESCRIPTION_PROPOSAL_KIND = 23
24: 'Allow event discussions',  // CHANGE_ALLOW_DISCUSSION_PROPOSAL_KIND = 24
25: 'Show event progress',  //CHANGE_HIDE_VOTING_PROPOSAL_KIND = 25
26: 'Upgrade repository tags', //TAG_UPGRADE_PROPOSAL_KIND = 26
27: 'Ask DAO membership allowance',  //ABILITY_INVITE_PROPOSAL_KIND = 27
-->

## __Voting procedure__
To vote for the proposal, some of your tokens must be be allocated to SMV (once the proposal is completed), you can get them back.

!!! info
    You can vote for a proposal only once.

For example, to merge into main, [create a pull request](../gosh-web/repository.md#create-pull-request) from some other branch. A proposal will be generated and will appear on the **DAO** tab.

<!-- TODO 
change images -->

<!-- ![](../../images/gosh_web_Voiting_SMV_01.jpg) -->

Open the proposal and review the contents.

<!-- ![](../../images/docker_ext_Voiting_SMV_02_proposal.jpg) -->

The voting period is indicated on the proposal page. This is the time allotted for [voting](../../on-chain-architecture/organizations-gosh-dao-and-smv.md#soft-majority-voting).

Unless a decisive majority of >50% Global Karma Count is achieved early, votes will be counted at the end of this period.

!!! info 
    Global Karma Count is the total amount of Karma calculated by summing up the Karma of all DAO members at the time of the proposal creation.

<!-- 
TODO update

Voting statistics are located under the status **Running**. The green and red counters indicate how many tokens have been used at the moment to vote for and against the proposal.

The green indicator in the top right corner means that the SMV smart contracts are not currently processing any new votes. It turns red when the SMV contracts are busy.

Once you have made a decision, select the amount of tokens with which you are ready to vote and click **Vote for proposal**


The red and green numbers next to **Running** status indicate how many tokens were used by now to vote for and against the proposal.

The green indicator in the top right corner means that the SMV smart contracts are not currently processing any new votes. It turns red when the SMV contracts are busy. -->

Once you have made a decision, input the amount of tokens, select **Approve** or **Reject** and click **Vote for proposal**. Vote registration can take a bit of time.

!!! info
    As per the rules of Soft Majority Voting, to have a proposal approved early, you need at least 50% of the total supply of tokens in the repository + 1 token used to vote for the proposal.

    For example, in a repository with two members, where the total supply of tokens is 200, 101 token needs to be used to instantly approve a proposal. Thus with every member holding 100 tokens a proposal can never be instantly completed without the participation of members other than the proposal's author.

    On the other hand, so as not to depend on all members of an organization to vote, soft majority vote will complete with an approval at the end of the voting period, if 10% of the total token supply were used to vote for, and no one voted against.

    The more tokens are sent against the proposal, the higher the approving amount needs to be (up to 50% of the total supply  + 1 token) for the proposal to pass.

Other members of the Organization, who have transferred their tokens to SMV, will be able to vote for the proposal on this page in their own accounts.

!!! info
    Currently, even in organizations with a single member, voting still takes place when a proposal is created. 51 tokens are needed to approve a proposal in such a repository.

Once a majority has been reached early, or the voting period ended and the soft majority vote result was decided, the proposal completes and the proposed action is performed.
<!-- ![](../../images/docker_ext_Voiting_SMV_03_result.jpg) -->

