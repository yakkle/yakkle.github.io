---
title: Go-ethereum
author: yakkle
date: 2022-04-04
category: Jekyll
layout: post
---


## Packages overview

| package          | description                                                                    |
|------------------|--------------------------------------------------------------------------------|
| account          | account management                                                             |
| build            | build package and CI                                                           |
| cmd              | cli tools (geth, evm, abigen, clef, devp2p, ...)                               |
| common           | various help function                                                          |
| consensus        | implements consensus engine                                                    |
| consensus/beacon | Proof Of Stake                                                                 |
| consensus/clique | [Proof Of Authority][Proof Of Authority]                                       |
| consensus/ethash | [Proof Of Work][Proof Of Work]                                                 |
| console          | JavaScript interpreted runtime environment(jsre)                               |
| contracts        | checkpointoracle?                                                              |
| core             | implements the Ethereum consensus protocol                                     |
| core/asm         | EVM assembly instructions                                                      |
| core/bloombit    | implements bloom filtering                                                     |
| core/forkid      | implements [EIP-2124]                                                          |
| core/rawdb       | collection of low level database accessors                                     |
| core/state       | caching layer atop Ethereum state trie                                         |
| core/types       | data types ethereum consensus                                                  |
| core/vm          | implements Ethereum Virtual Machine                                            |
| crypto           | secp256k1, blake2d, ...                                                        |
| eth              | implements Ethereum protocol                                                   |
| eth/catalyst     | implements Ethereum protocol                                                   |
| eth/downloader   | manual full chain synchronisation                                              |
| eth/ethconfig    | configuration of the ETH and LES protocols                                     |
| eth/fetcher      | announcement based header, blocks or transaction synchronisation               |
| eth/filters      | implements an ethereum filtering system for block, transactions and log events |
| eth/gasprice     | gas price                                                                      |
| eth/protocols    | eth, snap                                                                      |
| eth/tracers      | manager for transaction tracing engines                                        |
| ethclient        | client for Ethereum RPC API                                                    |
| ethdb            | defines the interfaces for an Ethereum data store                              |
| ethstats         | network stats reporting service                                                |
| event            | deals with subscriptions to real-time events                                   |
| graphql          | provides a GraphQL interface to Ethereum node data                             |
| internal         | ethapi, debug, jsre, web3ext, ...                                              |
| les              | implements the Light Ethereum Subprotocol                                      |
| light            | implements on-demand retrieval capable state and chain objects                 |
| log              | fork of [log15] library                                                        |
| metric           | fork of [go-metrics] library                                                   |
| miner            | implements Ethereum block creation and mining                                  |
| mobile           | simplified mobile APIs to go-ethereum                                          |
| node             | sets up multi-protocol Ethereum nodes                                          |
| p2p              | implements the Ethereum p2p network protocols                                  |
| params           | config, version, network param, protocol param                                 |
| rlp              | implements the RLP serialization format                                        |
| rpc              | implements bi-directional JSON-RPC 2.0 on multiple transports                  |
| signer           | core, fourbyte, rules, storage                                                 |
| trie             | implements Merkle Patricia Tries                                               |


<!-- Links -->
[Proof Of Authority]: https://eips.ethereum.org/EIPS/eip-225
[Proof Of Work]: https://eth.wiki/en/concepts/ethash/ethash
[EIP-2124]: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2124.md
[log15]: https://github.com/inconshreveable/log15
[go-metrics]: https://github.com/rcrowley/go-metricis