# Blockchain and Cryptocurrency

![bitcoin](https://cdn.rawgit.com/ShevaXu/blockchain-bitcoin/master/images/bitcoin-logo.svg)

This is my notes for taking the course [Bitcoin and Cryptocurrency Technologies](https://www.coursera.org/learn/cryptocurrency/home) by Princeton University since 2017-02-20.

## Week 4

> How to store & use ~~bitcoin~~ secret key

* availability
* security
* convenience

**Bitcoin wallet** - A piece of software that remembers an individual's Bitcoin addresses and keys.

### Hot & cold storage

*Separate keys for separate bitcoins (addresses)*

- hot storage - online, convenient but risky (the wallet)
- cold storage - offline, archival but safe (the safe)

:bulb: *Hierarchical key generation*

<img alt="hot and cold" src="https://cdn.rawgit.com/ShevaXu/blockchain-bitcoin/master/images/hot-cold.svg" width="400px">

What a paper wallet looks like (&copy; [bitcoinpaperwallet.com](https://bitcoinpaperwallet.com)):

![paper-wallet](https://bitcoinpaperwallet.com/images/front-back-sample-big.jpg)

:bulb: Key split & sharing - Split (share) secret into `N` pieces s.t. iff. given any `K` pieces can reconstruct the secret.

### Online Wallet, Exchange \& Payment

* Online Wallet (Services) - convenient, ideally run by security experts (https://bitcoin.org/en/choose-your-wallet)
* Bitcoin Exchanges - bank-like services `BTC <-> $` (https://blockchain.info/charts/market-price)
* Payment Services - merchants accepting BTC want `$`, *simple deployment* and *low risk (tech, security \& exchange-rate)*

> When you buy BTC, no transaction appears on the blockchain; the Exchange is just making a different promise.

Exchange's **Proof of Reserve** (independently verifiable using *Merkel-Tree*, no central regulator required):

- Prove that `>=x` amount of reserve currency 
- Prove that customers have `<=y` deposit
- So reserve fraction `>=x/y`

**Transcation Fee** `= value of inputs - value of outputs`

- goes to the miner recording the block (higher fee encourages faster relay \& record)
- concensus fee: 0.0001 BTC per 1000 bytes (no fee for some conditions)

Liquid Market (*supply vs demend* dynamic)

- Demend comes from:
	- fiat-currency transactions
	- investment
	- (arguably) paying transaction fee
- The equilibrium *price* `P = TD/S`
	- `T ($/sec)` total transcation value mediated via BTC 
	- `D (sec)` duration per transaction (almost fixed)
	- `S` supply of BTC excluding long-term investment (assumed fixed)

So `P` is proportional to `T` (\~ active transactions); but if more people prefer investment, price goes up as well .

Where to buy bitcoin :moneybag:

- online market: http://bitcoincharts.com/markets/
- p2p (https://localbitcoins.com/) and meetups

## Week 5

Bitcoin mining in 6 steps:

1. Join the network, listen to all transactions (and validate them);
2. Maintain the blockchain (listen and validate new blocks);
3. Assemble a new valid block;
4. **Find the `nouce` to make your block valid;** (`~2^66` trials)
5. Hope everyone accepts your new block;
6. Profit!

Difficulty: *10min/block* (adopted every two weeks, see the [trend](https://bitcoinwisdom.com/bitcoin/difficulty)) 

### Hardwares \& Energy

- ~~CPU mining~~
- ~~GPU mining:~~
	- Goodput - worth over-clocking 50% with 30% errors
	- Poor utilization of hardware, poor cooling and power efficiency
- ~~[FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array) mining~~
- Bitcoin ASICs ([application-specific integrated circuit](https://en.wikipedia.org/wiki/Application-specific_integrated_circuit))
	- e.g., TerraMiner IV since *Jan 2104*, `2 TH/s`, $6,000, ~14 months to find a block
	- most boards obsolete within 3~6 months (difficulty is dynamic based on total computation power) `->` **shipping is important**
	- Individuals should have lost money ... but bitcoin price is rising
- Professional mining centers (img &copy; [BitFury](http://bitfury.com/products#container-datacenter))

<img alt="mining center" src="http://bitfury.com/products/icblockbox_2.jpg" width="490px">

Energy:

- Embodied, electricity, cooling
- ~US$15,000/block (or 150~900MW electricity consumed)
- All (other) payment systems require energy
- Data fornaces `->` heater

### Strategies

Mining Pools \& Mining Shares

- Protocal, API, even hardware supports
- Pros: more predictable, good for small miners
- Cons: centralized, full nodes discouraged
- The [pools](https://bitcoinchain.com/pools)

Game-theoritic, strategic decisions:

- which transactions to include (*any above min tx fee*)
- which block to mine on top of (*longest valid chain*)
- how to choose between colliding blocks (*first heard*)
- when to announce a new block (*immediately after finding*)

> What you can do other than those default decisions?

- Forking attacks `->` crash exchange rate `->` destroy Bitcoin
	- enforce checking point
- Block-withholding (not announce immediately)
- Punitive-forking, feather-forking (blacklist tx from *X*, or negotiate tx fee)

> Miners are free to implement any strategy but little non-default behaviours in the wild so far.

## Week 6

`anonymity = pseudonymity + unlinkability`

Complete unlinkability is hard (only anomymity set)

* link different addresses of the same user
* link different transactions of the same user
* link sender of a payment to its recipient

Anonymity vs decentralization

* Interactive protocal with bank (e.g., blind signature) are hard to decentralize
* Decentralization often achieved via public traceability to enforce security

> Best practice: always receive at fresh address

* Application-layer de-anonymization
	- Shared spending is evidence of joint control ([An Analysis of Anonymity in the Bitcoin System](https://arxiv.org/abs/1107.4524) and its [blog](http://anonymity-in-bitcoin.blogspot.com/))
	- Change address - idioms of use ([A fistful of Bitcoins](http://cacm.acm.org/magazines/2016/4/200174-a-fistful-of-bitcoins/fulltext) and related  [blog](https://blog.acolyer.org/2017/02/20/a-fistful-of-bitcoins-characterizing-payments-among-men-with-no-names/))
* Network-layer de-anonymization (first node to infrom)

[Tor](https://www.torproject.org/) - anonymous communication (layered encryption)

- [Hidden services](https://www.torproject.org/docs/hidden-services.html.en) - silk road

### Mixing

- intermediary - online wallet requires trust
- delicated mixing services (no records \& identities, ~~laundry~~)
	- use a series of mixes (standard API)
	- uniform transactions (chunk size)
	- automated client
	- all-or-nothing fee
- currently no reputable delicated mix
- decentralized mixing - [CoinJoin](https://en.wikipedia.org/wiki/CoinJoin)
	- finding peers: using untrusted server
	- peer anonymity: routing
	- denial of service: *CoinShuffle* [pdf](https://petsymposium.org/2014/papers/Ruffing.pdf)
- high-level flows/patterns can be recognized - :bulb: *merge avoidance*

<img alt="coinjoin example" src="https://en.wikipedia.org/wiki/File:CoinJoinExample.svg" width="500px">

[**Zerocoin**](http://zerocoin.org/) - protocol-level mixing

- Cryptographic guaranteen of mixing (not Bitcoin-compatible)
- Extension of Basecoin (Bitcoin-like Altcoin)
- [Zero-knowledge proof](https://en.wikipedia.org/wiki/Zero-knowledge_proof): minting/commitment
- [*Zerocash*](http://zerocash-project.org/): without basecoin - ledger/blockchain merely records existance of transactions

System | Type | Attacks | Deployability |
---|---|---|---
Bitcoin|Pseudonymous|Tx graph analysis|Default
Single Mix|Mix|Tx graph analysis, bad mix|Usable today
Mix chain|Mix|Side channels, bad mixes/peers|Bitcoin-compatible
Zerocoin|Cryptographic mix|Side channel (possibly)|Altcoin
Zerocash|Untraceable|None|Altcoin, tricky setup

## Show Me the Codes

* https://github.com/bitcoin/bitcoin (Go) - *Bitcoin* source code.
* https://github.com/lhartikk/naivechain (JS) - See this [blog](https://medium.com/@lhartikk/a-blockchain-in-200-lines-of-code-963cc1cc0e54#.4mdlna763).
* https://github.com/IBM-Blockchain/learn-chaincode (Go) - Learn how to write chaincode.
* https://github.com/chain/chain (Go) - Chain Core Developer Edition.
* https://github.com/ethereum/go-ethereum (Go) - *Ethereum* protocol (for the blockchain platform).

Info APIs

* https://bitcoinchain.com/api REST, network status \& block info