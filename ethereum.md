# Ethereum

[Ethereum](https://www.ethereum.org/) and its founder [Vitalik Buterin](https://en.wikipedia.org/wiki/Vitalik_Buterin) (image from coinfox).

![buterin](http://www.coinfox.info/images/buterin111.jpg)

I like this simple explanation from [*What The Fuck Is Ethereum?*](http://whatthefuckisethereum.com/), when explain it like *I'm five*:

> Ethereum is a way for a bunch of computers to talk to each other. People can ask these computers to run programs that can't easily be shut down because all the computers share the code with each other.
>
> If you want to run a program that takes a long time to finish, you have to pay the computers in the network a currency called Ether.

## Intro

> What Bitcoin does for distributed data storage, Ethereum does for distributed data storage plus computations.

-|Description|Decentralization
---|---|---
Ethereum Virtual Machine| runs contract logic|computation
[Swarm](https://github.com/ethersphere/swarm)| Peer-to-Peer file sharing, similar to BitTorrent, but incentivised with micropayments of ETH. Files are split into chunks, distributed and stored with participating volunteers. These nodes that store and serve the chunks are compensated with ETH from those storing and retrieving the data.|storage
[Whisper](https://github.com/ethereum/wiki/wiki/Whisper)|an encrypted messaging protocol that allows nodes to send messages directly to each other in a secure way and that also hides the sender and receiver from third party snoopers.|communications

Accounts 

- only store ETH – known as Externally Owned Accounts (EOAs)
- store ETH and have code (smart contracts) that can be run – these smart contracts are activated by a transaction sending ETH into it

### v.s. Bitcoin

Similar to Bitcoin, Ethereum

- has a blockchain (https://etherscan.io);
- is public and permissionless;
- has Proof-of-Work (PoW) mining (so far);
- has an inbuilt cryptocurrency (*Ether*, ETH).

*But* Ethereum has

- **shorter** block time & **smaller** blocks;
- *Virtual Machine* that can run smart contracts;
- more complicated token issuance

![token-issuance](https://bitsonblocks.files.wordpress.com/2016/10/eth_vs_btc_issuance.png)

`#ETH` in existence are:

```
Pre-mine + Block rewards + Uncle rewards + Uncle referencing rewards
```

- Pre-mine: ~72 million ETH were created for the crowdsale in July/Aug 2014;
- Block reward: currently each block mined creates 5 fresh ETH;
- Uncles: blocks are mined a little late and don’t form part of the main blockchain ("orphans" in Bitcoin), can be referenced by later blocks:
	- the miner of the uncle gets 4.375 ETH if referenced as uncles by a later block;
	- a miner who references an uncle also gets 0.15625 ETH per uncle (maximum 2 uncles).

The miner of a block receives:

```
5(4.375) ETH (uncle) block reward + 
[2 * 0.15625 uncle referencing] +
[gas from contracts]
```

The data in uncles is not used, but
		
1. it incentivises miners to mine even though there is a high chance of creating a non-mainchain block
2. it increases the security of the blockchain by acknowledging the energy spent creating the uncle blocks

### History

[Launch process](https://blog.ethereum.org/2015/03/03/ethereum-launch-process/)

- **Olympic** (testnet): Launched May 2015 – a testing release where coins are not compatible with ‘real’ ETH. A testnet still runs in parallel to the main live network so that developers can test their code.
- **Frontier**: Launched 30 July 2015 – an initial live release with a way for people to mine ETH and build and run contracts.
- **Homestead**: Launched 14 March 2016 – some protocol changes, more stability.
- **Metropolis**: Future launch – moving from command-line to graphical interfaces.
- **Serenity**: Future launch – moving from Proof of Work (Ghost) to Proof of Stake (Casper).

Serenity is intended to have two major feature sets: [abstraction](https://blog.ethereum.org/2015/12/24/understanding-serenity-part-i-abstraction/), and [Casper](https://blog.ethereum.org/2015/12/28/understanding-serenity-part-2-casper/), our security-deposit-based proof of stake algorithm.

*Note*: [Ghost](https://github.com/ethereum/wiki/wiki/White-Paper#modified-ghost-implementation) protocol (Greedy Heaviest-Observed Sub-Tree)

#### ETH vs. Ethereum Classic (ETC)

[Why are There Now Two Ethereums?](http://www.investopedia.com/articles/investing/080516/why-are-there-now-two-ethereums.asp)

In short, a hacker found an exploit in TheDao's (Decentralized Autonomous Organization) smart contract code and stole tens of millions of dollars worth of Ethereum's virtual currency, which led to an unprescedented hard fork in the Ethereum blockchain in July 2015 that effectively reversed the transactions.

## Smart Contracts

Smart contracts are:

- pre-written logic (computer code),
- stored and replicated on a distributed storage platform (eg a blockchain),
- executed/run by a network of computers (usually the same ones running the blockchain),
- and can result in ledger updates (cryptocurrency payments, etc).

> If this happens then do that

#### Languages

- **Solidity** – similar to the language Javascript. This is currently the most popular and functional smart contract scripting language. ([*C++* source](https://github.com/ethereum/solidity), [doc](https://solidity.readthedocs.io)) and tutorials [ethereumdev.io](https://ethereumdev.io/)
- *Serpent* (like Python) and *LLL* (Lisp Like Language) are only used in the early days.
- [Viper](https://github.com/ethereum/viper) - New experimental programming language.

### Gas

When you activate a smart contract, you ask all the miners in the whole network to each individually perform the calculations within it by paying a small amount of ETH:

```
Payment (in ETH) = Gas amount (in Gas) x Gas price (in ETH/Gas)
```

- *Gas amount*: the more complex the smart contract (the number and type of computational steps, memory used for storage, etc), then the more Gas the contract requires to run and complete;
- *Gas Price*: Whereas the amount of Gas to run a contract is fixed for any specific contract, as determined by the complexity of the contract, the Gas Price is specified by the person who wants the contract to run, at the time they request it (a bit like Bitcoin transaction fees). Each miner will look at how generous the gas price is, and will determine whether they want to run the contract as part of the block. If you want miners to run your contract, you offer a high Gas Price. In this way it’s a competitive auction driven by how much someone is willing to pay to have a contract run.

*Why Gas?*

Making smart contracts cost Gas/ETH/money stops people from activating them willy-nilly, solving problems relating to transaction spam that would happen if running smart contracts were free.

## Software

### [Geth](https://github.com/ethereum/go-ethereum)

COMMAND LINE TOOLS FOR THE ETHEREUM NETWORK.

```
$ geth [--testnet] --fast --cache=512 console
```

This command will:

 * Start geth in fast sync mode (`--fast`), causing it to download more data in exchange for avoiding processing the entire history of the Ethereum network, which is very CPU intensive.
 * Bump the memory allowance of the database to 512MB (`--cache=512`), which can help significantly in sync times especially for HDD users. This flag is optional and you can set it as high or as low as you'd like, though we'd recommend the 512MB - 2GB range.
 * Start up Geth's built-in interactive [JavaScript console](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console), (via the trailing `console` subcommand) through which you can invoke all official [`web3` methods](https://github.com/ethereum/wiki/wiki/JavaScript-API) as well as Geth's own [management APIs](https://github.com/ethereum/go-ethereum/wiki/Management-APIs). This too is optional and if you leave it out you can always attach to an already running Geth instance with `geth --attach`.
 * `--testnet` flag connects to the test network instead, which uses different P2P bootnodes, different network IDs and genesis states (no *real-money*, play-Ether only).

`geth help` for more CLI [options](https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options).

The Ethereum Improvement Proposal ([EIPs](https://github.com/ethereum/EIPs)).

## Misc

### News

2017-07-21: [*A hacker stole $31M of Ether — how it happened, and what it means for Ethereum*](https://medium.freecodecamp.org/a-hacker-stole-31m-of-ether-how-it-happened-and-what-it-means-for-ethereum-9e5dc29e33ce)

> First, remember, this was not a flaw in Ethereum or in smart contracts in general. Rather, it was a developer error in a particular contract.

### Refs

Excerpt from:

- *[A gentle introduction to Ethereum](https://bitsonblocks.net/2016/10/02/a-gentle-introduction-to-ethereum/)*
- *[A gentle introduction to smart contracts](https://bitsonblocks.net/2016/02/01/a-gentle-introduction-to-smart-contracts/)*

Ecosystem:

- [Mist](https://github.com/ethereum/mist) browser - tool of choice to browse and use [Ðapps](http://dapps.ethercasts.com/) (read [*How to build server less applications for Mist*](https://blog.ethereum.org/2016/07/12/build-server-less-applications-mist/))
