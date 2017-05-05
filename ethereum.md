# Ethereum

https://www.ethereum.org/

## Intro

*This is mostly excerpt from [A gentle introduction to Ethereum](https://bitsonblocks.net/2016/10/02/a-gentle-introduction-to-ethereum/).*

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

## Smart Contracts

https://bitsonblocks.net/2016/02/01/a-gentle-introduction-to-smart-contracts/
