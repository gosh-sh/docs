# Git Open Source Hodler

(Yes, it's [Hodler](https://en.wiktionary.org/wiki/hodl){:target="_blank"}).

**GOSH** — a Decentralized Cloud to build consensus around your documents.

A Git on-chain and DAO platform, GOSH offers a suite of ready-to-use embedded applications to write and deploy code, conduct peer reviews, run decentralized [Hackathons and Grant Programs](hacks-and-grants/overview.md), and much more. GOSH is a Public Chain with [Ethereum L2](ethereum-L2/overview.md) cross-chain functionality, built on the groundbreaking [Acki Nacki](https://www.ackinacki.com/){:target="_blank"} consensus protocol, which supports a Freemium business model (gas-free transactions).

## Architecture

1. Build a scalable multithreaded, multisharded content addressable blockchain
2. Implement Git using [smart contracts](on-chain-architecture/gosh-smart-contracts.md)
3. Implement [DAO](on-chain-architecture/organizations-gosh-dao-and-smv.md) on top of that Git to allow building consensus around the code
4. Formally verify the smart contracts
5. Represent all entities by hashes (container images, git commits, blоbs, pull requests etc.);
6. Allow anyone to add some metadata with signature to any entity;
7. Allow anyone to decide whose metadata to trust;
8. Build chain/tree of trust: dependencies can be organized using the same architecture, and containers built

## Instruments and utilities

A variety of utility tools to assist with all the aspects of the solution are under active development. Explore the tools available now to get started with GOSH:

* create and manage your on-chain repositories using [GOSH Web](https://app.gosh.sh){:target="_blank"} or directly in the [Docker Extension](https://hub.docker.com/extensions/teamgosh/docker-extension){:target="_blank"}
* work with on-chain repository as if you use a regular git repository with [Git Remote Helper](working-with-gosh/git-remote-helper.md)
* To ensure the security of your software supply chain, you can use [AnyTree](working-with-gosh/anytree.md). This is a software deployment system that is secured by the blockchain.
<!-- * [build and sign](working-with-gosh/build-and-sign-images.md) images straight from GOSH -->
<!-- * [verify images](working-with-gosh/verify-images-in-docker-extension.md) -->
