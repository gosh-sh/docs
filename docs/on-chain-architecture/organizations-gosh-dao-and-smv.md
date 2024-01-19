# Organizations: GOSH DAO and SMV

## **DAO**


Every repository on [GOSH](../working-with-gosh/gosh-web/account.md#create-account) is managed as a [**Decentralized Autonomous Organization** - DAO](../working-with-gosh/gosh-web/create-dao.md) – a tool that allows every developer to build on GOSH in a way that is decentralized, secure, and scalable.

Every organization has, as a minimum, one member who [creates and manages repositories](../working-with-gosh/gosh-web/repository.md). However, once more than one [user is added to a DAO](../working-with-gosh/gosh-web/members.md#adding-members-to-dao), it is then governed through decentralized management mechanisms.

Your can [configure](../working-with-gosh/gosh-web/dao-set-up.md) your DAO easily.
The main of these mechanisms is voting. Any action in a DAO requires a vote and is created through [proposals](../on-chain-architecture/organizations-gosh-dao-and-smv.md#soft-majority-voting). For example, a user may propose to [commit of file](../working-with-gosh/gosh-web/repository.md#create-file) into a repository, and a soft-majority vote (SMV) of all other DAO members may be required to approve it. [Branches](../working-with-gosh/gosh-web/repository.md#​create-branch) could be locked to require any changes to them to be voted on by DAO SMV.


## **Soft Majority Voting**


Soft Majority Voting, or SMV for short, is a voting mechanism designed for transparency and optional participation.

The outcome of a Soft Majority Vote is decided by the difference between the number of votes for, and the number of votes against a proposal. If nobody objects, a minimum threshold of approving votes is required for the proposal to pass.

If everyone votes either for or against a proposal, 50% + 1 vote is required for the proposal to pass.

If the only votes given are for the proposal, and no one votes against, 10% approving votes are enough for the proposal to pass immediately.

Everything in between these two extremes is a linear dependency between the percentage of votes against and the percentage of votes for, that is required for the proposal to pass.

For important decisions a more strict super majority approval criteria may be set up.

![](../images/smv.png)

All SMV proposals have a set deadline. When it is reached, accumulated votes are counted, the decision is made, and the proposal pass.

If, however, a majority of 50% + 1 vote is reached early, the proposal passes immediately.


## **SMV in GOSH**


In GOSH one vote is one token.

### **Tokens and Karma**

The total supply of tokens is set when a DAO is created.

A DAO's first user automatically gets 20 DAO tokens and 20 Karma.

**Karma** is the amount of tokens (upper limit) within which a DAO member can vote.

Karma is either granted by a DAO decision upon member acceptance or earned through repository contribution.
This determines the reputation of a DAO member. The Karma can be changed only by voting.

See [here](../working-with-gosh/gosh-web/dao-overview.md) for more information.

### **Voting**
If several members jointly vote for a proposal with 50% + 1 token of the Global Karma Count of a DAO then the proposal passes early.

**Global Karma Count** is the total amount of Karma calculated by summing up the Karma of all DAO members at the time of the proposal creation.

If no one objects to a proposal for the duration of its voting period, 10% of the Global Karma Count is enough, but the proposal will only pass at the end of the voting period.

If votes are split, and neither side achieves 50% + 1 token early, the proposal completes at the end of the voting period and the result is calculated according to the SMV diagram above.
