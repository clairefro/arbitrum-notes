# arbitrum

Optimistic rollup L2 developed by Offchain Labs (NYC based)

What does that mean...
([source](https://coinmarketcap.com/alexandria/article/optimistic-rollups-for-the-rest-of-us))

- **Trustless**. Unlike traditional sidechains, ORUs are trustless (or, if you want to be technical, trust-minimized). You don't have to trust that a majority of the URU's block producers are honest to always be able to withdraw your funds from the rollup.

- **Permissionless**. Unlike Plasma, ORUs are permissionless. Anyone can produce a new block for an ORU since all the rollup block data is posted on Ethereum and available. The specifics of how to decide who the next leader is an implementation detail rather than a fundamental constraint.

- **Non-custodial**. Combining the above two properties, since an ORU is both trustless and permissionless, you can always withdraw your funds and no one can stop you. Therefore, they are non-custodial.

- **Expressive**. Unlike ZK rollups, ORUs allow (both in theory and in practice) for a high level of expressivity, ranging from Bitcoin-like UTXO payments to full-blown EVM-compatible execution.

- **Open participation**. Unlike channels, ORUs support smart contracts with open participation, like Uniswap.

- **Capital efficient**. Unlike channels, ORUs do not require that users lock up capital upfront.

- **Resistant to chain congestion**. Unlike channels and Plasma, ORUs are resistant to chain congestion, since fraud is proven at the block level rather than the channel closure or Plasma exit level.

- **No novel cryptography**. Unlike ZK rollups, ORUs do not require any novel cryptography.

- **Fast (but not instant) finality**. Unlike ZK rollups, there is no need to generate proofs, so ORU blocks can be posted to Ethereum immediately. Since valid ORU blocks can't be rolled back, they have the same finality guarantees as Ethereum as soon as they're posted to Ethereum.

## Rollup

= off-chain aggregation of transactions in an Ethereum smart contract. Increased throughput of blockchain to higher tps. Publishes just enough data on-chain so observer can reconstruct state ([source](https://medium.com/interdax/ethereum-l2-optimistic-and-zk-rollups-dffa58870c93))

Concept started in 2014, described as "shadow chains" by Vitalik

Data validation still occurs on Ethereum main chain.

## Optimistic rollups (ORUs)

### Merged consensus

Objective deterministic permissionless consensus protocol that can be used for side chains. Verifiable entirely **on-chain**

[Mnimum viable spec](https://ethresear.ch/t/minimal-viable-merged-consensus/5617)

> The consensus protocol for optimistic rollup runs entirely on-chain in a smart contract; hence, it does not affect or require support from the main chain’s consensus rules ([source](https://medium.com/@adlerjohn/the-why-s-of-optimistic-rollup-7c6a22cbb61a))

More [here](https://coinmarketcap.com/alexandria/article/optimistic-rollups-for-the-rest-of-us); deep dive [here](https://medium.com/@adlerjohn/the-why-s-of-optimistic-rollup-7c6a22cbb61a)

## Aggregators and Validators

- aggregators: incentivised with network fees
- and validators: incentivised in a similar way to full nodes in bitcoin

> When aggregators get sufficiently many state updates, they’ll put this in a block and register the block on the Rollup contract (shown in Figure 6). Aggregators put up a bond, so if they put an invalid transaction into a block, they will get slashed and lose their bond. If the bond is high enough, then the risk for the average user should be close to nothing.

([Source](https://medium.com/interdax/ethereum-l2-optimistic-and-zk-rollups-dffa58870c93))

## Optimistic vs. ZK rollups

[Source](https://medium.com/interdax/ethereum-l2-optimistic-and-zk-rollups-dffa58870c93)

> In contrast to ZK-Rollups, Optimistic Rollups are assumed to be correct until someone proves it is wrong.

### Validity assurance

- Optimistic: fraud proof and the synchrony assumption
- ZK: zero-knowledge proofs

> A zero-knowledge proof simply demonstrates that you know some secret to someone else without revealing the secret itself. Through virtue of mathematics, the verifier can check that the prover knows the secret without it actually being revealed to them.

## EVM compatibility

- Optimistic: almost anything possible in Ethereum to be possible in the OVM, including the composability of smart contracts. 80% tooling transfer
- ZK: ZK-Rollups are only currently effective for payments and a few other use cases

## Challenges

**Optimistic**

> - The more volume a single Rollup has, the less validators can run the full node, meaning that it is less secure to rely on the 1-of-N honest assumption

> - Also, it is not yet known with certainty what the ideal parameters are for the bond requirement and the window of time before blocks are finalised. For existing implementations, bond requirements vary between 1 ETH and 32 ETH. Some projects will use a delay of 1–2 weeks, while there’s also an argument for times as short as three hours. Improving capital efficiency will require a shorter window, leading to a tradeoff between capital efficiency and security.

> - To get around this, there is scope to introduce market makers into Optimistic Rollups to provide liquidity for fast exits, where a user will pay a fee to finalise their transaction and exit the Rollup. But then this creates a two-tier system: faster settlement for those who are willing to pay for an exit, and slower settlement for those who stay on the Optimistic Rollup until a block is finalised.

> **ZK**
> The major challenge for ZK-Rollups is integrating smart contract functionality:

> - atter Labs’ ZK-Rollup implementation, zkSync, is working to make this possible so that developers can take any existing contract written in Solidity/Vyper and deploy it to zkSync with minimum modifications.

> - Another challenge relates to computation. Currently, zero-knowledge proofs are quite computationally intense, but the goal for the future is to bring block confirmations from around 20 minutes to less than a minute.

> - Another limitation of ZK-Rollups is the reliance on a trusted setup of ZK-SNARKs, which will be addressed in the future as work on ZK-STARKs progresses and as these proofs are made more efficient.
