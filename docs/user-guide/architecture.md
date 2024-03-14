
1. Build a scalable multithreaded, multisharded content addressable blockchain
2. Implement Git using [smart contracts](../on-chain-architecture/gosh-smart-contracts.md)
3. Implement [DAO](../on-chain-architecture/organizations-gosh-dao-and-smv.md) on top of that Git to allow building consensus around the code
4. Formally verify the smart contracts
5. Represent all entities by hashes (container images, git commits, blobs, pull requests etc.);
6. Allow anyone to add some metadata with signature to any entity;
7. Allow anyone to decide whose metadata to trust;
8. Build chain/tree of trust: dependencies can be organized using the same architecture, and containers built
