# BigchainDB Roadmap

Below is a sketch of some of the things we plan to do in upcoming releases of BigchainDB Server (and associated software), i.e. in the near term. It is, of course, subject to change. If you don't see an important feature listed here, please read about how to request a feature in our docs on [Contributing to BigchainDB](https://docs.bigchaindb.com/projects/contributing/en/latest/index.html).

## BigchainDB 2.0

The main change in BigchainDB 2.0 (from 1.3) is that consensus, replication and sync are done using Tendermint. That means that [BigchainDB 2.0 is Byzantine Fault Tolerant (BFT)](https://blog.bigchaindb.com/bigchaindb-2-0-is-byzantine-fault-tolerant-5ffdac96bc44).

Starting with BigchainDB 2.0, we commit to making it possible to migrate to the next version without loss of data. We will provide documentation and tools to help with migration. This is needed by users who are going into production.

### Done in BigchainDB 2.0 Alpha, Released on April 3, 2018

1. Finish HTTP API changes
1. Simplify & automate the production deployment process
1. Consolidate the proposal system (especially COSS)
1. Change the allowed transaction version number from "1.0" to "2.0"
1. Update the official drivers (Python driver & JavaScript driver)
1. BigchainDB Server CLI updates (not the client-side CLI: deprecate that)
1. Compute an app hash for Tendermint (in a dumb way _that works_).
1. Standard process to set up a local node for development & testing, using Docker Compose.
1. Set up a network for the AE team to do some performance tests.
1. New `bigchaindb upsert-validator` subcommand to add/change/remove a validator at run time, "insecure" way.
1. The Events API ane Events Plugin API: update code & docs.

### Done in BigchainDB 2.0 Alpha 2, Released on April 18, 2018

1. Implement [BEP-8](https://github.com/bigchaindb/BEPs/tree/master/8).
1. Provide more informative HTTP responses when posting transactions.

### Done in BigchainDB 2.0 Alpha 3, Released on May 3, 2018

1. Fix all priority-0 bugs, such as [issue #2182](https://github.com/bigchaindb/bigchaindb/issues/2182).
1. Integrate the latest verson of Tendermint. This means upgrading the ABCI server software used by BigchainDB (py-abci).
1. In our production deployment template, combine Tendermint and BigchainDB inside _one_ Kubernetes StatefulSet (a kind of pod, one with persistent state).
1. Documentation about how a node operator can expose the full power of MongoDB to users.

### Done in BigchainDB 2.0 Beta 1, Released on June 1, 2018

1. Have a second, internal test network, where each node is operated by a different BigchainDB employee.
1. Update the Ansible & Vagrant deployment tooling.
1. Remove some dead code, e.g. the code for RethinkDB support, and the "pipelines" code.

### Done in BigchainDB 2.0 Beta 2, Released on July 16, 2018

1. The test networks have run without issue for weeks.
1. Performance optimization by fixing the MongoDB index on transaction id.
1. New BigchainDB configuration settings: Tendermint host and port.
1. Made changes to BigchainDB to keep up with changes in Tendermint.
1. Remove a lot of dead code, e.g. the code for voting & blocks.

### Done in BigchainDB 2.0 Beta 3, Released on July 18, 2018

Fixed a bug in transaction validation.

### Done in BigchainDB 2.0 Beta 4, Released on July 30, 2018

1. Implement a clean shutdown procedure for BigchainDB.
1. Monit script to manage both BigchainDB and Tendermint as a single service unit.
1. Some tests cleanup.
1. Implement BEP-14 in the Python driver.

### Goals for the Final Stable Release of BigchainDB 2.0

There's a loose collection of some BigchainDB 2.0 "TODO" items in the GitHub organization project board named BigchainDB 2.0 TODO: https://github.com/orgs/bigchaindb/projects/5

1. Have a way to add/remove/update a validator at run-time (maybe by making `bigchaindb upsert-validator` work). This is [issue #2372](https://github.com/bigchaindb/bigchaindb/issues/2372).
1. Create and run more performance tests (benchmarks) and stress tests. Publish all testing software and test results.
1. Migration to future versions should be possible: write about _how_ to do that in various cases. See the explanation of what that means in the first paragraph of this section. See [BEP-42](https://github.com/bigchaindb/BEPs/tree/master/42). Implement BEP-42 and test that implementation.
1. A single Docker container containing BigchainDB, Tendermint and MongoDB. See https://github.com/bigchaindb/bigchaindb/pull/2424
1. Make changes to keep up with changes in Tendermint before the release of Tendermint 1.0. See the Cosmos Roadmap page (https://cosmos.network/roadmap) and issue https://github.com/tendermint/tendermint/issues/1568
1. Add a BigchainDB Server configuration setting for maximum allowed transaction size (using Gunicorn).
1. Tests cleanup. See [issue #2381](https://github.com/bigchaindb/bigchaindb/issues/2381).
1. Implement BEP-14 in the JavaScript driver.
1. (Maybe) Add support for MongoDB authentication by username & password.
1. (Maybe) Change the Dockerfile to use the Alpine (minimal) base image.

## Some Goals for BigchainDB 2.1 and Beyond

- Document how to run a production validator so that it's protected from denial-of-service (DoS) attacks and similar issues. See what Tendermint recommends (i.e. "sentry nodes", see issue https://github.com/bigchaindb/bigchaindb/issues/2333).
- Performance optimization by removing unneeded deepcopy operations.
- Example projects showing how to use BigchainDB with other decentralized systems, especially Ethereum.
- Refactoring, especially of the transaction-related code.
- New way to compute the app hash based on the UTXO set, including an efficient way to update the Merkle tree used to compute the app hash from the UTXO set.
- No more 3scale (currently used by the BigchainDB Testnet)
- Support hashlock conditions (securely: need to make sure that every transaction is still signed by a client)
- Support timelock conditions
- (?) LevelDB vs other backends in Tendermint?
- Plugins/extensions for specialized use cases
- Smart contract support. (Not necessarily within BigchainDB; maybe just better documentation about how to integrate with other smart-contract blockchains.)
- Test what happens when a node runs out of memory or hard drive space. For example, what happens when there's no more space for MongoDB to write a block?

## BigchainDB 3.0?

- Make it possible to run a public BigchainDB network where anyone can add a node (without permission).
