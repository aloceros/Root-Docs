# Root Token

A robust decentralized governance mechanism must balance the principles of decentralization with resistance to attempted protocol changes, both malicious and ignorant, and the ability to quickly adapt to changing information. **Root’s Stalk ownership gives Root a vote in Beanstalk governance.**

In theory, Root should balance ensuring sufficient time for all Root owners to consider a Root Improvement Proposal (RIP) and cast their votes or exit the system, with the abilities to (1) be quickly upgraded in cases of emergency and (2) participate in Beanstalk governance.

In practice, the owner of Root has the exclusive and unilateral ability to commit RIPs, and vote in Beanstalk governance, at any time. The owner of each implementation of Root enforces a governance mechanism.

[Root](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26) is governed by Root DAO. Root DAO governs upgrades to [0x77700005BEA4DE0A78b956517f099260C2CA9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26), the use of Stalk in Beanstalk governance and the treatment of non-Beanstalk-native yield earned by [0x77700005BEA4DE0A78b956517f099260C2CA9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26). Any account that owns Roots can participate in Root DAO governance.

RIPs are proposed on the[ Root DAO Snapshot page](https://snapshot.org/#/rootsmoney.eth). Root owners can vote on RIPs on the Snapshot page.

## Root Improvement Proposals&#x20;

Root is an upgradable contract. Root uses OpenZeppelin’s UUPS implementation. A RIP has 2 inputs: (1) a new contract address and (2) an optional function call.

## Participation&#x20;

Any account that owns Roots can participate in Root governance. Any account can become a Root Holder and participate in Root governance by Minting Roots for Beanstalk Silo Deposits on the Minting Whitelist through Root at any time. Any account that owns more than 0.1% of total outstanding Roots can submit a RIP to the Root DAO Snapshot via the Root DAO Multisig (RDM). A Root holder’s voting power is proportional to their Root balance relative to the total Root supply.

Root DAO only accepts votes in favor of RIPs. An account’s vote for a given RIP is counted as the minimum of its Roots between the beginning and end of the Voting Period.

## Voting Period&#x20;

A Voting Period begins when a vote for a RIP can be submitted to Snapshot and ends at approximately the beginning of the 168th Beanstalk Season after it begins, or when the RIP is committed with a supermajority.

If at the end of the Voting Period:

* Less than or equal to half of the total outstanding eligible Roots votes in favor of the RIP, it fails; and
* More than half of the total outstanding eligible Roots votes in favor of the RIP, it passes.&#x20;

If at any time before the end of the Voting Period more than two-thirds of the total outstanding eligible Root votes in favor of the RIP, it passes and the RDM can commit and execute the RIP on-chain.

## Stalk Use

In its capacity as a Stalkholder, [0x77700005BEA4DE0A78b956517f099260C2CA9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26) is entitled to vote on (1) each Beanstalk Improvement Proposal (BIP) and (2) other, non-BIP, governance processes, and may be entitled to non-Beanstalk- native yields.

Any Root owner can propose a Root Stalk Proposal (RSP) on the [RSP Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) to determine how Root should use its Stalk in each governance process, and distribute yields, if ever. RSPs follow the same structure as RIPs, except that the length of the Voting Period can be reasonably shortened to ensure the will of Root DAO can be reflected in the governance process when appropriate.&#x20;

Any Beanstalk Improvement Proposal (BIP) will automatically qualify to be proposed to Root DAO as an RSP.

The RDM will participate in each governance process as determined by the RSP.

## Commit

The RDM address has the exclusive and unilateral ability to commit RIPs and participate in Beanstalk governance, at any time. In the future, it is expected that a RIP will revoke these abilities from the RDM and reimplement on-chain governance. You can read more about the RDM [here](rdm-process.md).
