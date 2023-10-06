# EP-2: ISO15022/20022 and MT format support

## Index

[About project](https://github.com/olegasivakov/ep-2#about-project)
- [Motivation](https://github.com/olegasivakov/ep-2#motivation)
- [Project plan](https://github.com/olegasivakov/ep-2#project-plan)
- [Project importance](https://github.com/olegasivakov/ep-2#project-importance)
- [Issues](https://github.com/olegasivakov/ep-2#issues)
- [Competition](https://github.com/olegasivakov/ep-2#competition)

[Technical overview](https://github.com/olegasivakov/ep-2#technical-overview)
- [Usecases](https://github.com/olegasivakov/ep-2#usecases)
- [Context](https://github.com/olegasivakov/ep-2#context)
- [Technical analysis](https://github.com/olegasivakov/ep-2#technical-analysis)
- [DOD](https://github.com/olegasivakov/ep-2#dod)
  - [Stage 1](https://github.com/olegasivakov/ep-2#stage-1)
  - [Stage 2](https://github.com/olegasivakov/ep-2#stage-2)
  - [Stage 3](https://github.com/olegasivakov/ep-2#stage-3)
  - [Stage 4](https://github.com/olegasivakov/ep-2#stage-4)
  - [Stage 5](https://github.com/olegasivakov/ep-2#stage-5)
  - [Stage 6](https://github.com/olegasivakov/ep-2#stage-6)
- [Estimated time](https://github.com/olegasivakov/ep-2#estimated-time)
- [How to test](https://github.com/olegasivakov/ep-2#how-to-test)
- [How to deploy](https://github.com/olegasivakov/ep-2#how-to-deploy)

[Usage](https://github.com/olegasivakov/ep-2#usage)

[Notes](https://github.com/olegasivakov/ep-2#notes)

[License](https://github.com/olegasivakov/ep-2#license)

## About project

### Motivation

We intend to make Ethereum-based blockchains compliant to international financial messaging standards.

ISO 15022/20022, known as "universal financial industry message scheme", offers business modeles and data design rules related to financial market. Business modeles includes securities operations, payments, trade services, Forex, cards and related services. MT messages format ("SWIFT" messages) is a proprietary data format developed and used by SWIFT, the international provider of secure financial messaging service.

Blockchain now has many intersections with regulated financial institutions that use mentioned standards of data messaging. We believe that intersections will deeper and business possibilities will greater when regulated institutions and crypto enthusiasts start using common messaging standards. In particular, this means that the blockchain node should _(a)_ read standartized messages from off-chain financial information systems, _(b)_ respond to, and _(c)_ send to off-chain standartized messages based on the results of transaction execution.

We started developing this project in order to provide blockchain businesses and software developers with the possibility of direct integration of on-chain and off-chain information systems.

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

At the end, we have to provide instructions and examples for community of developers (maybe, including some of business models provided by ISO 15022/20022?), and Docker container of node and external services supported ISO 15022/20022 and MT messages for blockchain.

### Project importance

There is a wide list of important points of implementing ISO financial standards in Ethereum.

ISO 15022/20022 brings standardization and interoperability to the crypto space, ensuring smoother communication between various platforms and participants. It provides a common language and structure for the exchange of electronic data between financial institutions and international payment systems like SWIFT. More than 70 countries made their regulations compliant to international standard.

**1. Common points of importance:**

- **Interoperability**: ISO 20022 compliance enhances compatibility between cryptocurrencies and traditional financial systems, enabling seamless cross-network transactions.
- **Institutional Integration**: Adhering to ISO 20022 standards makes it easier for institutional players to integrate cryptocurrencies into their existing systems, potentially increasing adoption.
- **Global Acceptance**: ISO 20022’s recognized framework can boost the legitimacy of digital currencies, fostering broader acceptance and presumably increasing their value.
- **Efficient Communication**: Standardized messaging reduces complexities in communication, streamlining processes and reducing errors in crypto transactions.
- **Cross-Border Transactions**: ISO 20022 compliance simplifies cross-border crypto transactions, as the standardized format is understood worldwide.
- **Innovation Pathway**: Embracing ISO 20022 demonstrates cryptocurrency’s willingness to align with modern financial practices, encouraging further innovation and partnerships.
- **Regulatory Alignment**: Compliance with recognized financial standards may lead to smoother regulatory relationships, aiding in addressing potential concerns.
- **Enhanced Data Management**: Standardized data formats facilitate better data management and analysis, enabling improved insights into cryptocurrency markets.
- **Market Growth**: ISO 20022-compliant cryptocurrencies could attract more investors and traders, contributing to increased market liquidity and growth.
- **Mainstream Exposure**: Integration with a well-established standard brings cryptocurrencies closer to mainstream financial services and presumably broader user bases.

**2. Importance for community of developers:**

- **Interoperability for development**: 

**3. Importance for crypto-business community**

- **Business models**: Well-developed business models compliant to world-wide regulations

**4. Importance for crypto users**

**5. Importance for integrators:**

**6. Importance for financial institutions:**

**7. Importance for authorities:**

### Issues

During the project we plan to solve the next issues:

- make the Top-1 business blockchain compatible with international financial messaging standard,
- provide smoothly and secure communications between on-chain and off-chain information systems,
- and bring together communities of crypto- and institutional developers by offering a set of development and integration tools.

### Competition

There are not too many blockchains already compliant to international financial standards: Quant (QNT), Ripple (XRP), Stellar (XLM), Hedera (HBAR), IOTA (MIOTA), XDC Network (XDC), Algorand (ALGO). XRP is only part of Top-10 of cryptocurrencies by Coinmarketcap (QNT, the next, is 42nd); and XRP is only moving to regulatory compliance in some countries.

Being the Top-1 of business blockchains, Ethereum will be the first of Top-10 blockchains compatible with international standards and regulations.

## Technical overview

### Usecases

We develop this project for the next usecases:

**1. Buy, sell, transfer, deposit, pledge a native coin or stablecoin defined by smart contract**

**2. Fiat payment and exchange fiat currencies**

**3. Issue, buy, sell, transfer, deposit, pledge securities defined by smart contract**

Another usecases should be implemented later using development tools.

### Context

### Technical analysis

**1. Data processing**

Ethereum blockchain provides data broadcast, access and execution layer using as a basement for external business logic. Any operation inside that layer is processed by sending ```transaction```, a structured data including node coin value, input data, and a number of technical fields.

There are two common cases of transaction usage:

- sending coins (```ETH``` or ```wei```) from user's account to another account;
- sending some data to execution layer oа blockchain, expecting that this data will be accepted and processed by the ```contract```.

ISO 15022/20022 and MT messages are looks like as:

- a set of data that can be splited to sender-related, receiver-related, and customer-related prtis,
- coin transfer instructions, containing a wide amount of data in a comparision with traditional ```Ethereum``` transaction data,
- a set of data that should be processed by some algorithm (```contract```, for example). This data set may contain a dictionary- or library-related data (may be indexed), and a customer-related (individyally-defined) data.

All data of standartized messages should be securely transferred; in common case, it means that data should be encrypted, but the blockchain ```contract``` should process data despite that encryption. It means that one of particular tasks is to create an ```object``` that can be processed with contract uzing **zero-knowledge** approach to data processing.

Solving our issues with data processing, we have to make improvements to the node that can parse standartized message, translate it to the `blockchain` standard, and vice versa after the message was processed with transaction.

**2. Connections and cybersecurity**

Blockchain is a network of untrusted nodes; it means that we don't need to monitor network security issues when the transaction was signed and sent to blockchain. But, we have to build a strong security for network between off-chain information systems and ethnode, including node itself.

Typically, Ethnode is running on the single device (PC or server), or in the Docker container. It can recieve CLI or RPC (HTTP, WS, IPC) requests using Ethereum native format. Ethnode can broadcast signed externally-formed transactions to blockchain network; it is also available to sign transactions when method ```personal_unlockAccount()``` previously called.

**3. Data formats**

**4. Sender, receiver, customer identities**

**5. Development tools**

### DOD

#### _Stage 1_

#### _Stage 2_

#### _Stage 3_

#### _Stage 4_

#### _Stage 5_

#### _Stage 6_

### Estimated time

### How to test

_@TODO_

### How to deploy

_@TODO_

## Usage

_@TODO_

## Notes

> [!NOTE]
> ISO 20022 official website: https://www.iso20022.org/

> [!NOTE]
> ISO 20022 Intellectual property rights information: https://www.iso20022.org/intellectual-property-rights

## License

[![GitHub license](https://img.shields.io/badge/license-MIT-lightgrey.svg?maxAge=2592000)](https://raw.githubusercontent.com/apollostack/apollo-ios/master/LICENSE)

MIT
