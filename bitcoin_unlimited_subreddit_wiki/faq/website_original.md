## Original BU website FAQ

This page contains the FAQ content from the original BU website at 
https://www.bitcoinunlimited.info/faq .

This content is parked here prior to being integrated into the new
structured Wiki FAQ.

### Q[ae9956]: Will unlimited size blocks actually result in no fee market?

No. Intuitively you can understand this by realizing that it will take a lot longer to propagate a gigantic block across the network than a small one. Therefore a gigantic block has a higher likelihood of being "orphaned" -- that is, a competing block will be found, propagated across the network and supplant the gigantic block. In this case the miner of the gigantic block will lose the block subsidy and transaction fees. Therefore miners are incentivised by limitations in the underlying physical network to produce smaller blocks, and incentivized by transaction fees to produce larger ones.

Finding the balance between these forces is where the free market excels. As underlying physical networks improve or fees increase, miners will naturally be able to produce larger blocks. The transaction "supply" (space in a block) therefore depends directly on the fundamental capacity, rather than relying on some centralized "steering committee" to properly set maximum block size. Bitcoin is all about disintermediation, and this is another example of it working.

For a formal treatment of this subject see [A Transaction Fee Market Exists Without a Block Size Limit.](https://www.bitcoinunlimited.info/resources/feemarket.pdf)


### Q[9d804c]: Will unlimited size blocks actually result in gigantic blocks?

No. The effective network throughput is currently limited by the production of single transaction (empty except for the coinbase) blocks. The larger blocks get, the more of these blocks are generated, resulting in a maximum average block size. Additionally a rational miner should not accept a gigantic block since it denies him any chance to also produce transaction-containing blocks. More specifically, if the expected time to find and validate a short block is lower than the time to validate the gigantic block, it maximizes revenue to continue to mine a sibling while simultaneously validating the gigantic block.

For a formal treatment of these subjects see [An Examination of Single-Transaction Blocks and Their Effect on Network Throughput and Block Size.](https://www.bitcoinunlimited.info/resources/1txn.pdf)


### Q[8ffc8a]: Why is a formal Bitcoin Unlimited Articles of Federation necessary?

It is completely unknown whether the majority of Bitcoin users support a block size greater than 1 MB. No formal debate or vote has occurred. In contrast, debate is censored on the two most popular Bitcoin community sites.

A majority of miners have "voted" for the unimplemented BIP100 proposal (this proposal would then allow miners to vote on block size), yet nothing has been done to implement BIP100. The existence of BIP100, BIP101 and other proposals may be "splitting" the large max-block community -- yet there is no known mechanism to authoritatively retire a proposal so the community can converge on a single proposal. As such, individuals who have contributed a vast amount of time and energy to a particular implementation/BIP find themselves without recourse as the power to add or remove features rests solely with individuals who possess technical skills and were at the right place at the right time.

_When you switch to the Bitcoin Unlimited client, the Articles of Federation will ensure that your voice is heard, and your vote counted._

Proposals are made, debated, and then resolved (voted on) and the Proposer and BU officers have the power to force this process to occur in a timely fashion. The Articles also ensure that passed, implemented proposals are committed to the code repository in a timely fashion.

For more information please read the [Bitcoin Unlimited Articles of Federation](https://www.bitcoinunlimited.info/articles)


### Q[17ba6e]: Is BU going to fork the Blockchain?

No. But if some other entity causes a fork, if for example miners start producing > 1MB blocks, then Bitcoin Unlimited nodes will follow the most-work (generally the longest) fork. This means that your BU node will track the mining majority rather then a specific choice.

Right now, the only event that will trigger this behavior is a block size fork because we believe that the block size is NOT part of blockchain consensus. If other events that are currently part of "consensus layer" should also trigger this behavior they may be added based on the outcome of a BUIP (Bitcoin Unlimited Implementation Proposal) submission, debate and vote.


### Q[7f4d01]: Does BU open up a new Sybil attack vector? Say some entity launches thousands of nodes, 60,000 for example (100x the current network levels). Then sets a super small blocksize. Does this not end up holding the network hostage and thus also the blocksize cap?

Nodes have this power and therefore the network is vulnerable to this kind of attack with or without BU. If you have the resources and desire to launch 60,000 nodes, a few changes to the source code will not put you off -- having access to BU is irrelevant.


### Q[1c4cf5]: Can miners run BU, select a very small block limit and therefore reduce transaction supply below 1MB?

If 51% of the miners want smaller blocks they can have them today without BU. They can simply limit the size of their generated blocks -- the max mined block size is a command line option. Also, the max block size to accept is a constant defined in a header file. So 1 simple line of code needs to be changed for miners to ignore blocks bigger than N in all the "Satoshi-derived" clients.


### Q[5b81b3]: Does BU affect blockchain consensus? Is it possible for a network filled with BU nodes to not converge?

If you set certain parameters to certain values you can, for example, mimic the behavior of Bitcoin Core. Bitcoin Core will not converge in a network with miners producing blocks that are both greater than and less than 1 MB (this is called a fork).

Let us imagine a BU-only network with the excessive block size set at 1 MB for many nodes, and blocks being produced at both less than 1MB and greater than 1MB. This network will converge rapidly if there is a large disparity in hash power between the two groups. The larger block nodes "sees" the smaller chain and will switch to it right away if it takes the lead. The smaller block group "sees" the larger chain but will resist switching to it until additional blocks have been built on top of it. So the smaller block group may always be a few blocks behind and small block miners will produce many orphans. The opposite is true in the case where large block miners are the hash power minority, except that they are always at the head of the most-work chain. This orphan production is feedback mechanism the network uses to the miners to change their behavior.

If the two groups have approximately equal hashing power, the situation becomes a [random walk](https://en.wikipedia.org/wiki/Random_walk) due to the fact that block production is a Poisson process. In this case, the mathematics show that one fork will periodically move far enough ahead of the other to trigger a convergence.

If the network is undergoing a period of block size instability, whether that be due to a struggle between two block-size-is-part-of-consensus clients like XT and Core or due to a struggle between miners of similar hash power, it may make sense for users to wait for additional confirmations or convergence to avoid double spends.

In Bitcoin Unlimited, we hope to eventually track ALL nontrivial forks and visually indicate when transactions have been confirmed on all forks, eliminating the possibility of a double spend. This will allow users to use the bitcoin network normally during these periods. However, since we do not believe that these periods will last long because they will cause a dramatic drop in miner revenue, it is not a priority.
