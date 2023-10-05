# EP-2: ISO15022/20022 and MT format support

## About project

### Motivation

ISO 15022/20022, known as "universal financial industry message scheme", offers business modeles and data design rules related to financial market. Business modeles includes securities operations, payments, trade services, Forex, cards and related services. MT messages format ("SWIFT" messages) is a proprietary data format developed and used by SWIFT, the international provider of secure financial messaging service.

Blockchain now has many intersections with regulated financial institutions that use mentioned standards of data messaging. We believe that intersections will deeper and business possibilities will greater when regulated institutions and crypto enthusiasts start using common messaging standards. In particular, this means that the blockchain node should _(a)_ read standartized messages from off-chain financial information systems, _(b)_ respond to, and _(c)_ send to off-chain standartized messages based on the results of transaction execution.

I started developing this project in order to provide blockchain businesses and software developers with the possibility of direct integration of on-chain and off-chain information systems.

### Project plan

Our target is to teach the ethereum node to:
- receive and parse ISO 15022/20022 and MT messages,
- translate it to transaction pre-validating one (and encrypt it?),
- split standartized data to tx body and tx data intended for smart contracts,
- reduce on-chain data using specialized smart contracts as common dictionaries and data libraries,
- sign and send well-formed blockchain transaction responding by standartized message,
- detect on-chain messages addressed to accounts of this node, read (and decrypt?) and parse result of transaction execution as formed as ISO 15022/20022 or MIT data standard,
- create standartized message and send it to on-chain,
- use a version control approach for data schemes, dictionaries and data libraries.

We have to describe usecases, and develop the testing environment to demonstrate data transfers related to provided usecases.

Working on above, we have to solve some problems related to authorizing the external service to sign blockchain transaction, translate standartized messages to the blockchain transaction and vice versa, and authorize blockchain node to connect to external service. In particular, we should follow to one of financial cybersecurity frameworks and develop a lot of papers (threat model, etc.).

At the end, we have to provide instructions and examples for community of developers (maybe some of business models provided by ISO 15022/20022?), and Docker container of node and external services supported ISO 15022/20022 and MT messages for blockchain.

### Project importance

### Issue

### Competition

## Technical overview

### Usecases

### Context

### Technical analysis

### DOD

### Estimated time

### How to test

### How to deploy

## Usage

## Notes

## License

[![GitHub license](https://img.shields.io/badge/license-MIT-lightgrey.svg?maxAge=2592000)](https://raw.githubusercontent.com/apollostack/apollo-ios/master/LICENSE)

MIT
