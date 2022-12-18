# Proposals

This page is a comprehensive overview of all proposals types as it pertains to governance of Root.

### Table of Contents

* [Notes](proposals.md#notes)
* [Root Improvement Proposal](proposals.md#rip) (RIP)
* [Root Stalk Proposal](proposals.md#rsp) (RSP)

## Notes

In all cases:

* A Root Holder's vote for a given proposal is counted as their minimum Roots between the beginning and end of the Voting Period, or **Voting Roots**;
* 1 Voting Root equals 1 vote;
* Voting Abstain is equivalent to voting Against;
* The Root being used in the Snapshot vote must not be corrupted by multi-block MEV or any other similar manipulation around the block indicating the beginning of the Voting Period; and
* The proposer must meet the minimum Root threshold to propose at both the beginning and end of the Voting Period (in Voting Root terms).

All past proposals can be read [here](https://github.com/RootToken/Root-Governance-Proposals).

## Root Improvement Proposal <a href="#rip" id="rip"></a>

Root Improvement Proposals, or RIPs, are proposals to change Root or Root governance. Any Root Holder that owns at least 0.1% of total Roots can propose a RIP. Any Root Holder can vote For or Abstain.

The Voting Period opens when the Snapshot proposal for a RIP can be voted on and closes after 7 days or when it is committed with a supermajority.&#x20;

If at the end of the Voting Period:&#x20;

* Less than or equal to 50% of the total Voting Roots votes For the RIP, it fails, or&#x20;
* More than 50% of the total Voting Roots votes For the RIP, it passes.&#x20;

If at any time 24 hours or more after the beginning and before the end of the Voting Period more than two-thirds of the total Voting Roots votes For the BIP, the Root DAO Multisig (RDM) can execute the RIP.

BIPs are proposed on the [Root DAO Snapshot page](https://snapshot.org/#/rootsmoney.eth). Past BIPs can be read [here](https://github.com/RootToken/Root-Governance-Proposals/tree/main/rip).&#x20;

See [#rip-proposal-process](root-token/rdm-process.md#rip-proposal-process "mention") in [RDM Process](root-token/rdm-process.md) for more information on proposing a RIP.

## Root Stalk Proposal <a href="#rsp" id="rsp"></a>

Root Stalk Proposals, or RSPs, are proposals to determine how Root should use its Stalk to vote in non-BIP governance proposals, and distribute yield, if ever. Any Root Holder can propose a RSP and vote For or Abstain.

The Voting Period for RSPs is 7 days by default but can be reasonably shortened to ensure the will of Root DAO can be reflected in the governance process.

If at the end of the Voting Period:&#x20;

* Less than or equal to 50% of the total Voting Roots votes For the RSP, it fails, or&#x20;
* More than 50% of the total Voting Roots votes For the RSP, it passes.&#x20;

RIPs are proposed on the [Root Stalk Proposals Snapshot page](https://snapshot.org/#/rootstalkproposals.eth). Past RSPs can be read [here](https://github.com/RootToken/Root-Governance-Proposals/tree/main/rsp).

See [#rsp-proposal-process](root-token/rdm-process.md#rsp-proposal-process "mention") in [RDM Process](root-token/rdm-process.md) for more information on proposing a RSP.
