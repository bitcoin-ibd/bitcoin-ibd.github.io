# Welcome to Bitcoin-IBD

Bitcoin-IBD is a community-powered project to collect as much information about the Initial Blockchain Download (IBD) times of Bitcoin across as many devices and networks as possible. This will be useful for community decision-making around the healthiness of the block size. 

This organisation will be maintained by Bitcoin community members. 

Please [view the form here](https://docs.google.com/forms/d/e/1FAIpQLSeDonDOT0As3Yb0_Byk4QBDT91W4vUtqQIVUaR2uLuPHiWlPQ/viewform).

Data will be [publicly collected here](https://docs.google.com/spreadsheets/d/1zv0RcRIkX9IJRnlesnYC9pQIImaAcGEcBjn4sKW3Yng/edit?usp=sharing).

Data will be [exported and held here](https://github.com/bitcoin-ibd/bitcoin-ibd.github.io/tree/master/data)

Please download the [Bitcoin Client here](https://bitcoin.org/en/bitcoin-core/). 

## Bitcoin will fail without decentralisation

Bitcoin is not what any individual, company or state says it is. It is what we all say it is; it is a meme, a shelling point, a majority consensus around money. You add your voice to the chorus of what Bitcoin is when you download the blockchain and run a full node - using the ruleset you choose to run. 

Bitcoin is an [impenetrable fortress of validation](https://hackernoon.com/bitcoin-miners-beware-invalid-blocks-need-not-apply-51c293ee278b). When you run a node you contribute to the maintenance of the shelling point; your node only relays blocks that are validated by the ruleset you choose. 

Bitcoin miners do not maintain the shelling point - they simply follow it wherever it goes. If a bitcoin miner submits a block that is invalid and not relayed by the economic majority of nodes, then it will not be propogated and they have wasted their time and resources. Put simply, miners secure transactions *that have been added to the blockchain*, whilst nodes decide what transactions *should be added to the blockchain*. **Miners face backwards, nodes face forwards.** 

If Bitcoin is to scale *and still be decentralised* to the world, then we need to address the IBD - the biggest burden on node operators. If 4bn people want to use Bitcoin in a few decades time, then it is preposterous to think that Bitcoin's primary line of defence against attacks, node operators, will only number in the 10's or 100's of thousands. Millions of people should be able to run nodes. 

To get the first million nodes online, the bitcoin community needs to guide Bitcoin to a point where low-power, low-cost devices can safely maintain a Bitcoin full node. Pruned nodes and even [Nuetrino](https://github.com/lightninglabs/neutrino) is not a solution since these nodes cannot participate in seeding the blockchain to new nodes. 

The blockchain is a product of waste that is a consequence of a fully audited supply and a validated transactional ledger. Every byte stored on it will be carried around forever by nodes. We must use the block space carefully and avoid wasteful transactions, especially careless uses of OP_RETURN and other data-insertion methods. 

Decentralisation of the Bitcoin blockchain is a cornerstone fundamental of Bitcoin ever since [Satoshi's whitepaper](https://bitcoin.org/bitcoin.pdf). Without decentralisation, the Bitcoin project will fail.


## Why is IBD a concern?

Initial blockchain download time is the biggest burden on new nodes. The process of IBD is as follows:

1) **Ping** New nodes ping the network for peers to download the blockchain (from a list of peers)

2) **Header Download** Nodes begin downloading the headers for each blockchain. Headers are fairly lightweight - [80 bytes each.](https://bitcoin.stackexchange.com/questions/48420/what-hardware-requirements-does-a-spv-client-have?rq=1) SPV clients stop here, since they can derive their own transactions from just the headers.*

3) **Block Download** Nodes then begin downloading the blocks, starting at Genesis. This is bandwidth constrained. Each block contains the full transaction set for each block.

4) **Block Validation** Nodes then begin validating each transaction for compliance with [the ruleset](https://github.com/bitcoin/bitcoin/blob/master/src/consensus/tx_verify.cpp). Validation is fast at first since each block generally only contained coinbase transactions. Validation slows down markedly beyond the 200k blockheight mark due to more complex transactions being included. The validation is as follows:
  - Load the downloaded transaction set into RAM (RAM bound)
  - Validate the transaction. (CPU bound)
  - Write to disk. (Disk I/O bound)
  
Low power devices, such as a RPi connected to a 1TB SATA disk, generally have low amounts of RAM (1gb), a low-power CPU (1.2Ghz ARM) and slow disk IO of around [120mbps](https://www.amazon.com/Seagate-Portable-External-Drive-STGX1000400/dp/B07CRG7BBH/ref=sr_1_1_sspa?keywords=1tb+seagate&qid=1549926521&s=gateway&sr=8-1-spons&psc=1). 

Doing a full validation from a RPi takes weeks weeks, since the IBD is constrained by validation (RAM and CPU) and disk IO, and not necessarily network download speed. The rate of innovation in these aspects (RAM, CPU and disk IO) is what is causing IBD concerns.

Currently this is leading to node operators to download a pre-validated bootstrap file from another source. This is not the desired behaviour and is a massive risk to true decentralisation. An example of this is the [CASA Node](https://store.casa/lightning-node/), a largely popular RPi-based node, which ships with a pre-validated blockchain running node software decided by the CASA team. If CASA rapidly commericialises this, the next million node operators will be spoon-fed a blockchain and node ruleset decided by a profit-motivated team. This is a serious problem. 

The Bitcoin community needs to strive to guide Bitcoin to a point where it is useable with the *lowest* common denominator, which is a low power device of similiar specs above. At the current rate of blockchain growth, getting Bitcoin working on low power devices is quickly slipping from our reach.

## Project

This project will be conducted in the following manner:

1) A bitcoin-ibd client will be produced to allow users to easily run an IBD test

2) IBD data will be collected on a public google form

3) IBD data will be held in a public google sheet

4) Project contributors will export data to the github repo, and display it on a public github page

Anyone can assist or contribute to this project. More info will be shown soon. 

******

All information and data in connection with this project is in the public domain. 
