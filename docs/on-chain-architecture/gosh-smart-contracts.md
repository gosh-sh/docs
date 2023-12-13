# GOSH smart contracts

GOSH is open-source and freely available on GitHub 

<!-- and, obviously, on GOSH. -->

**GOSH is the most secure Git Implementation in existence.**  
It stores, manages and processes all the editable GIT objects entirely on-chain. It verifies the correctness of all object mutations by invoking automatic checks and verifications by smart contracts.  

GOSH provides developers with a secure and transparent platform to collaborate on open-source projects and ensure the security of their software development and delivery as part of the software supply chain.

This is the general scheme of interaction between GOSH smart contracts:


<figure markdown>
  [![The general scheme of the interaction of GOSH smart contracts](../images/general%20scheme%20mini.png){ width="300" }](../images/general%20scheme.png)
  <figcaption></figcaption>
</figure>


GOSH consists of the following contracts (latest version):

* [VersionController ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/versioncontroller.sol)- a contract version manager used when upgrading GOSH smart contracts
* [SystemContract ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/systemcontract.sol)- main contract for hosting any specific version of GOSH smart contracts
* [Profile ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profile.sol)- a contract for a user's profile on GOSH
* [ProfileIndex](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profileindex.sol) - a contract for each user's public key
* [ProfileDao ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/profiledao.sol)- a contract of a DAO's profile on GOSH
* [GOSHWallet ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/goshwallet.sol)- user wallet for all user interactions with GOSH
* [GoshDao ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/goshdao.sol)- a contract storing organizations' objects
* [Repository ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/repository.sol)- a contract storing repositorys' objects
* [Commit ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/commit.sol)- a contract storing commits' objects
* [Tree ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/tree.sol)- a contract storing trees' objects
* [Diff ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/diff.sol)- a contract storing diffs' objects
* [Snapshot ](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/snapshot.sol)- a contract storing snapshots' objects
* [Tag](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/tag.sol) - a contract storing gits' tag object
* [DaoTag](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/daotag.sol) - a contract responsible for tags in a DAO
* [RepoTagGosh](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/taggosh.sol) - a contract responsible for tags in a repository
* [Task](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/task.sol) - a contract storing a task object
* [Topic](https://github.com/gosh-sh/gosh/blob/dev/v6_x/v6.2.0/contracts/gosh/topic.sol) - a contract storing the description of an object



<!-- 
TODO 
change github-links to gosh-links -->


