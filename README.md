# EP-2: ISO 15022 and ISO 20022 formats support for Ethereum

## Index

[About project](https://github.com/olegasivakov/ep-2#about-project)
- [Motivation](https://github.com/olegasivakov/ep-2#motivation)
- [Project plan](https://github.com/olegasivakov/ep-2#project-plan)
- [Project importance](https://github.com/olegasivakov/ep-2#project-importance)
- [Interested parties](https://github.com/olegasivakov/ep-2/blob/main/README.md#interested-parties)
- [Issues](https://github.com/olegasivakov/ep-2#issues)
- [Competition](https://github.com/olegasivakov/ep-2#competition)

[Technical overview](https://github.com/olegasivakov/ep-2#technical-overview)
- [Usecases](https://github.com/olegasivakov/ep-2#usecases)
- [Context](https://github.com/olegasivakov/ep-2#context)
- [Technical analysis](https://github.com/olegasivakov/ep-2#technical-analysis)
- [DOD](https://github.com/olegasivakov/ep-2#dod)
  - [Stage 1](https://github.com/olegasivakov/ep-2#stage-1-messaging-format-parser-and-translator-node-api-and-oracle-on-the-node)
  - [Stage 2](https://github.com/olegasivakov/ep-2#stage-2-message-encryption-and-decryption-version-contol-for-messages-on-chain-data-reduction-dictionaries-libraries-contract-interaction)
  - [Stage 3](https://github.com/olegasivakov/ep-2#stage-3-cybersecurity-format-manager-testing-environment-and-examples)
- [Estimated time](https://github.com/olegasivakov/ep-2#estimated-time)
- [How to test](https://github.com/olegasivakov/ep-2#how-to-test)
- [How to deploy](https://github.com/olegasivakov/ep-2#how-to-deploy)

[Usage](https://github.com/olegasivakov/ep-2#usage)

[Notes](https://github.com/olegasivakov/ep-2#notes)

[License](https://github.com/olegasivakov/ep-2#license)

## About project

### Motivation

We intend to make Ethereum-based blockchains compatible with international financial messaging standards.

ISO 15022/20022, known as "universal financial industry message scheme", offers business modeles and data design rules related to financial market. Business modeles include securities operations, payments, trade services, Forex, cards and related services. ISO 15022 MT messages format ("SWIFT" messages) is a proprietary data format developed and used by SWIFT, the international provider of secure financial messaging service.

Blockchain now has many intersections with regulated financial institutions that use ISO 15022/20022 messaging standards. We believe that intersections will deeper and business possibilities will greater when regulated institutions and crypto enthusiasts start using common messaging standards. In particular, this means that the blockchain node should _(a)_ read standartized messages from off-chain financial information systems, _(b)_ respond to, and _(c)_ send to off-chain standartized messages based on the results of transaction execution.

We're starting development of this project in order to provide blockchain businesses and software developers with the possibility of direct integration of on-chain and off-chain information systems.

### Project plan

Our target is to make the ethereum node capable to:
- [ ] receive and parse ISO 15022/20022 messages,
- [ ] turn it to transaction with pre-validation (and encryption?),
- [ ] split standardized data to tx body and tx data for smart contracts,
- [ ] reduce on-chain data using specialized smart contracts as common dictionaries and data libraries,
- [ ] sign and send well-formed blockchain transaction based on the standardized financial messages,
- [ ] detect on-chain messages addressed to accounts of this node, read (and decrypt?) and parse result of transaction execution as formed as ISO 15022/20022 data standards,
- [ ] create standardized message and send it to on-chain,
- [ ] use a version control approach for data schemes, dictionaries and data libraries.

We have to describe usecases, and develop the testing environment to demonstrate data transfers related to the provided usecases.

Working on the above, we have to solve some problems related to the authorization of external service to sign a blockchain transaction turning standartized messages to the blockchain transaction and vice versa, as well as the authorization of blockchain node to connect to the external service. In addition, we must follow one of the financial cybersecurity frameworks and develop a lot of papers (threat model, etc.).

Finally, we have to provide instructions and examples for community of developers (maybe, including some of business models provided by ISO 20022?), as well as Docker container for node and external services supporting ISO 15022/20022 messages for blockchain.

### Project importance

There is a wide list of important points of implementing of ISO financial standards in Ethereum.

ISO 15022/20022 brings standardization and interoperability to the crypto space, ensuring smoother communication between various platforms and participants. It provides a common language and structure for the exchange of electronic data between financial institutions and international payment systems like SWIFT. More than 70 countries made their regulations compliant to international standard.

- **Interoperability**: ISO compliance enhances compatibility between cryptocurrencies and traditional financial systems, enabling seamless cross-network transactions.
- **Institutional Integration**: Adhering to ISO standards makes it easier for institutional players to integrate cryptocurrencies into their existing systems, potentially increasing adoption.
- **Global Acceptance**: ISO’s recognized framework can boost the legitimacy of digital currencies, fostering broader acceptance and presumably increasing their value.
- **Efficient Communication**: Standardized messaging reduces complexities in communication, streamlining processes and reducing errors in crypto transactions.
- **Cross-Border Transactions**: ISO compliance simplifies cross-border crypto transactions, as the standardized format is understood worldwide.
- **Innovation Pathway**: Embracing ISO demonstrates cryptocurrency’s willingness to align with modern financial practices, encouraging further innovation and partnerships.
- **Regulatory Alignment**: Compliance with recognized financial standards may lead to smoother regulatory relationships, aiding in addressing potential concerns.
- **Enhanced Data Management**: Standardized data formats facilitate better data management and analysis, enabling improved insights into cryptocurrency markets.
- **Market Growth**: ISO-compliant cryptocurrencies could attract more investors and traders, contributing to increased market liquidity and growth.
- **Mainstream Exposure**: Integration with a well-established standard brings cryptocurrencies closer to mainstream financial services and presumably broader user bases.

### Interested parties

- Ethereum develiopers community, including developers of the Ethereum itself, Ethereum and Web-3 applications developers;
- Crypto-business community (may also be interested in the well-developed business models compliant to world-wide regulations offered by ISO 20022);
- Crypto users;
- System integrators;
- Financial institutions including banks, investment funds, brokers and traders, institutional investors, etc.;
- Finansial and economy authorities.

### Issues

During the project we plan to do as follows:

1) Make the Top-1 business blockchain compatible with international financial messaging standard,
2) Provide smoothly and secure communications between on-chain and off-chain information systems,
3) Bring together communities of crypto- and institutional developers by offering a set of development and integration tools.

### Competition

There are not many blockchains already meet the international financial standards: Quant (QNT), Ripple (XRP), Stellar (XLM), Hedera (HBAR), IOTA (MIOTA), XDC Network (XDC), Algorand (ALGO). XRP is only part of Top-10 of cryptocurrencies by Coinmarketcap (QNT, the next, is in the 5th dozen).

Being the Top-1 busines blockchain, Ethereum will be the first of the Top-10 of all blockchains that becomes compatible with international standards of financial messaging.

## Technical overview

### Usecases

We develop this project for the next usecases:

1. Buy, sell, transfer, deposit, pledge a native coin or stablecoin defined by smart contract
2. Fiat payment and exchange fiat currencies
3. Issue, buy, sell, transfer, deposit, pledge securities defined by smart contract

Another usecases should be implemented later using development tools.

### Context

### Technical analysis

**1. Data processing**

Ethereum blockchain provides data broadcast, access and execution layer using it as a basis for external business logic. Any operation inside that layer is processed by sending ```transaction```, a structured data including coin value, input data, and a number of technical fields.

There are two common usecases of transaction usage:

- sending coins (```ETH``` or ```wei```) from a user account to another account;
- sending some data to the execution layer oа blockchain, expecting that this data will be accepted and processed by the ```contract```.

ISO 15022/20022 messages looks like this:

- a set of data that can be divided to sender-related, receiver-related, and customer-related parts,
- coin transfer instructions, containing a wide amount of data in a comparision with traditional ```Ethereum``` transaction data,
- a set of data that should be processed by some algorithm (```contract```, for example). These data fields may contain a dictionary- or library-related data (may be indexed), and a customer-related (individyally-defined) data.

All contents of standartized messages should be securely transferred; in common case, it means that data should be encrypted, but the blockchain ```contract``` may process data despite that encryption. It means that one of particular tasks is to create an ```object``` that can be processed by the contract uzing **zero-knowledge** approach to data processing.

Solving mentioned issues of data processing, we have to make improvements to the node that can parse standartized message, translate it to the `blockchain` standard, and vice versa after the message was processed with transaction.

**2. Connections and cybersecurity**

An information system supporting the financial messaging standards must comply with cybersecurity frameworks related to financial market (such as ISO27k, NIST 800-171, GOST R 57580). These tasks should be correlated with blockchain context.

Blockchain is a network of untrusted nodes; it means that we don't need to track network security issues when a transaction has been signed and sent to the blockchain. ut we must ensure reliable protection of the network between off-chain information systems and the Ethnode, including the node itself.

In common case, Ethnode is running on a single device (PC or server), or in a Docker container. It can recieve CLI or RPC (HTTP, WS, IPC) requests using Ethereum native format. Ethnode can broadcast signed (externally-formed) transactions to blockchain network; it is also available to sign transactions when method ```personal_unlockAccount()``` was previously called. Access to this method is critical for all security levels.

The common solution is that the information system from (including) off-chain server to (including) node and from node to off-chain client must be the atomically isolated service. Off-chain components of this service should work as a firewall and a secure gateway between the unrusted blockchain network and the internal information system of financial organization.

**3. Data formats**

ISO 15022/20022 data formats have been officially published. Due to the large number of data schemas, we need to choose the schemas that will be implemented first; implementation of another ones will be available using format manager tools.

In addition, ISO 20022 contains descriptions of business models and operation flows. Some ones will be implemented in testing environments.

> [!NOTE]
> ISO 20022: XSD schemes defined for this standard
> 
> ISO 15022 MT list: 101, 103, 202, 900, 910, 940, 942, 950

**4. Sender, receiver, customer identities**

The ideology of financial messages is to transfer data of the identified user between identified and authorized participants of the financial data network. Blockchain network, at the same time, does not provide for the disclosure of information other than the public cryptographic key. ISO 15022/20022 format implementation should include ways to identify the addressee; perhaps this solution should also comply with the blockchain ideology of non-disclosure of the user's identity.

### DOD

#### _Stage 1. Messaging format parser and translator, node API and oracle-on-the-node_

- [ ] On-chain messaging format description;
- [ ] Node improvement module (rel. to [EP-21](https://github.com/olegasivakov/ethereum_projects_about/blob/main/README.md#ep-21-ethereum-node-extensions-node-improvement-module) ?), including:
  - [ ] node API component,
  - [ ] ISO 15022 parser and builder (prototype for to 8 messaging formats; will be replaced in the future to XSD schemes parser on the next stages),
  - [ ] ISO 20022 parser and builder (prototype for to 10 messaging formats defined in XSD schemes; will be replaced in the future to XSD schemes parser on the next stages),
  - [ ] transaction builder,
  - [ ] oracle server on-the-node;
- [ ] ISO 15022 gateway hosted on ```localhost```;
- [ ] ISO 20022 gateway hosted on ```localhost```;
- [ ] System manager (including configuration);
- [ ] Smart contract templates for ISO 15022/20022 formats;

_This list will extend if need._

#### _Stage 2. Message encryption and decryption, version contol for messages, on-chain data reduction (dictionaries, libraries), contract interaction_

- [ ] Contract data format description;
- [ ] Transaction data encryption and decryption (rel. to [EP-13](https://github.com/olegasivakov/ethereum_projects_about/blob/main/README.md#ep-13-encrypted-tx-data) ?);
- [ ] XSD schemes and XSD parser and builder for ISO 15022;
- [ ] XSD schemes parser and builder for ISO 20022;
- [ ] Dictionary and library contract templates;
- [ ] Improvements (related to contract data interaction) to ISO 15022/20022 parser and builder;

_This list will extend if need._

#### _Stage 3. Cybersecurity, format manager, testing environment and examples_

- [ ] Threat model and ISO27k controls implementation documentation;
- [ ] External service authorization manager;
- [ ] CS controls implementation (ISO 27001:2005 app.А5-А15)
- [ ] Messaging format manager tool;
- [ ] Docker container for entire system (node including improvement module, ISO and MT gateways)
- [ ] Testing environment;
- [ ] Example sets for usecases on JS, Python.

_This list will extend if need._

### Estimated time

**Stage 1 ETA**

1) On-chain messaging format description (p.1 of the plan of my project)
Result: documentation (including diagrams and its description) published in the Github repository of the project
Duration: 1 two-weeks sprint

2) Node improvement module (p.2, including subitems)
Result: sourcecode (node additions and complement courcefiles) published in the Github repository of the project. Includes node API component; parser and builder for a basic set of standardized messages; transaction builder and transaction parser; callback server ("oracle-on-the-node" server)
Duration: 5 two-weeks sprints

3) Gateway server (p.3 and 4) and System manager (p.5)
Result: sourcecode of gateway server for localhost including external and node communication I/O modules for ISO 15022/20022 messages, and a System managing module with configuration module
Duration: 2 two-weeks sprints

4) Smart contracts templates
Result: templates for smart contracts supporting standardized financial messages
Duration: 2 two-weeks sprints

5) Testing and and improvements
Result: updates to sourcecode of the above items published in the Github repository of the project
Duration: 2 two-weeks sprints

Total: 24 weeks (12 two-week full sprints)

**Stage 2 ETA**

_@TODO_ will be defined after Stage 1 completion

**Stage 3 ETA**

_@TODO_ will be defined after Stage 1 or 2 completion

### How to test

_@TODO_ will be defined (updated) for each stage

### How to deploy

_@TODO_ will be defined (updated) for each stage

## Usage

_@TODO_ will be defined (updated) for each stage

## Notes

> [!NOTE]
> ISO 15022 official website: https://www.iso15022.org/

> [!NOTE]
> ISO 20022 official website: https://www.iso20022.org/

> [!NOTE]
> ISO 20022 Intellectual property rights information: https://www.iso20022.org/intellectual-property-rights

## License

[![GitHub license](https://img.shields.io/badge/license-MIT-lightgrey.svg?maxAge=2592000)](https://raw.githubusercontent.com/apollostack/apollo-ios/master/LICENSE)

MIT
