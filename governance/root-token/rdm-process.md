# RDM Process

{% hint style="info" %}
In an attempt to facilitate a secure and transparent multisig process, the Root DAO Multisig (RDM) follows similar processes followed by the [Beanstalk Community Multisig](https://docs.bean.money/governance/beanstalk/bcm-process).
{% endhint %}

The RDM has the exclusive and unilateral ability to submit and commit RIPs, and vote on BIPs. The RDM is a Gnosis Safe multisig wallet with anonymous signers consisting of community members and contributors to Root and Beanstalk. Its m-of-n configuration will start as 4-of-7 on Ethereum mainnet. Parameters m and n are each ultimately defined by Root holders and may evolve in the future via Snapshot vote.

The RDM will provide sufficient notice of the submission of a RIP, its contents and the beginning of its Voting Period before submitting a RIP to Snapshot, and will repost BIPs on the [RSP Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) as soon as possible after they are posted to the [Beanstalk DAO Snapshot page](https://snapshot.org/#/beanstalkdao.eth).

## **Multisig Powers**

Root is an upgradable contract that uses [OpenZeppelin’s UUPS](https://docs.openzeppelin.com/contracts/4.x/api/proxy#UUPSUpgradeable) implementation.

The mechanism for upgrading Root is by calling either `upgradeTo()`, which takes an argument of the new implementation address, or `upgradeToAndCall()`, which takes arguments of a new implementation address and an optional function call. The `upgradeTo()` and `upgradeToAndCall()` functions will only be callable by the owner of Root, which will be the RDM.

Upgrades should only be executed after a Snapshot has passed and Signers have manually reviewed the code changes. However, in the case of an emergency (like a serious bug or exploit), the RDM may execute transactions to protect the Root contract. The best practices for emergency response handling are outlined in the [#emergency-response-procedures](rdm-process.md#emergency-response-procedures "mention") section.

If a community member wants to propose a RIP, they can submit a pull request to the [Root Token Github repo](https://github.com/RootToken) and begin a formal process with the RTM outlined in the [#proposing-a-rip](rdm-process.md#proposing-a-rip "mention") section.

The following functions are also only callable from the owner address:

* `upgradeTo()` —  Upgrade Root Token contract to a new implementation address.
* `upgradeToAndCall()` — Upgrade Root Token contract to a new implementation address and/or execute and init function with a delegatecall.
* `transferOwnership()` — Nominate a candidate to become the new owner of the Root Token contract. The new Nominated candidate will then need to call `claimOwnership()` before ownership of the contract is transferred.&#x20;
* `renounceOwnership()` — This function is currently disabled so calling it will revert. The function is still there because the ownership contract is inherited from OpenZeppelin.
* `addWhitelistToken()` — Add a token to the Minting Whitelist.
* `removeWhitelistToken()` — Remove a token from the Minting Whitelist.
* `setDelegate()` — Delegate Snapshot Stalk voting power of the Root contract.

## **Snapshots**

The RDM is an extension of Root DAO. As such, the RDM’s role is to 1) enact on-chain the decisions Root holders make via off-chain voting and 2) review and verify proposals to ensure the suggested changes are truthfully represented.

RIPs are voted on at the [Root DAO Snapshot page](https://snapshot.org/#/rootsmoney.eth).

The RTM shall not execute transactions until an associated Snapshot successfully passes in favor of the proposal, except in the case of emergency, cancelling a failed transaction or adding/removing/rotating RTM Signers. Below are the scenarios the RTM will adhere to when transacting:

| Transaction                                  | Snapshot | Voting Period                                                                                                           |
| -------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| Proposing RIP                                | Yes      | Up to 168 Beanstalk Seasons as outlined in the [#proposing-a-rip](rdm-process.md#proposing-a-rip "mention") section     |
| Proposing RSP                                | Yes      | Up to 168 Beanstalk Seasons as outlined in the  [#about-rsp-process](rdm-process.md#about-rsp-process "mention")section |
| Adding/Removing/Rotating RTM Signers         | No       | N/A                                                                                                                     |
| Emergency hotfix (needs public notification) | No       | N/A                                                                                                                     |
| Cancel Transaction                           | No       | N/A                                                                                                                     |

## Proposing a RIP

Root’s governance is modeled after Beanstalk’s governance. Root governance is designed to be as censorship resistant as possible. Any community member may submit RIPs. If a community member wishes to propose a RIP, they will need to complete a public proposal process on Discord and submit a Github pull request before the RDM will submit a Snapshot on their behalf.

#### **RIP Proposal Process**

RIPs consist of two things: (1) a pull request on the public Root Token Github repo, and (2) a written explanation of the changes that would be implemented by the pull request.

The following are the processes in place for community members to submit a RIP and coordinate with the RDM to submit a Snapshot proposal:

1. A proposer must own 0.1% of the total Root supply in order to propose a RIP. The proposer shall verify that they meet the Root ownership threshold by creating and verifying a signature on etherscan. The steps to create and verify a signature on etherscan can be found here. The proposer will then reach out to Root on Discord and from there, the RDM will verify that the address that signed the message has sufficient Stalk.
2. The proposer will submit a pull request on the public Root Token Github repo and publish the written proposal in a dedicated channel in the Root Discord. For assistance creating a channel on Discord, contact Root on Discord.
3. The written proposal shall be discussed in the Discord channel for a sufficient amount of time. What constitutes sufficient will be at the sole discretion of the RDM, but the RDM must formally propose the RIP on-chain within 2 weeks of the creation of the dedicated Discord channel, unless the proposer decides to withdraw their proposal.
4. RDM key holders shall verify that they have access to their wallets.
5. The RDM will submit a Snapshot of the written proposal and a corresponding on-chain transaction to formally begin the Voting Period.
6. During the Voting Period (1-7 days), every RDM Signer shall verify the transaction and write an etherscan message confirming their review according to the process outlined in the [#reviewing-and-signing-off-on-transactions](rdm-process.md#reviewing-and-signing-off-on-transactions "mention") section. Each Signer is expected to verify every transaction. However, if not all Signers verify the transaction, the RDM may still continue per the process outlined in the [#rotating-holders-in-out](rdm-process.md#rotating-holders-in-out "mention") section.
7. If the Snapshot passes, the Signers will sign m/n signatures and execute the transaction on-chain as soon as possible. If the Snapshot fails, the Signers will submit and execute a cancel transaction with the same nonce as soon as possible.

#### **About RSP Process**

In its capacity as a Stalkholder, [0x77700005BEA4DE0A78b956517f099260C2CA9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26) is entitled to vote on (1) each BIP and (2) other, non-BIP, governance processes, and may be entitled to non-Beanstalk-native yields.

Root Stalk Proposals (RSPs) are proposals for [0x77700005BEA4DE0A78b956517f099260C2CA9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26) to determine how Root should use its Stalk in each governance process, and distribute yield, if ever.

Any BIP will automatically qualify to be proposed to Root DAO as an RSP. The RDM will repost BIPs on the [RSP Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) as soon as possible after they are posted to the [Beanstalk DAO Snapshot](https://snapshot.org/#/beanstalkdao.eth/) page. The RDM will vote on each BIP as determined by the RSP.

For other governance processes, any Root holder can propose a Root Stalk Proposal (RSP) on the [RSP Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) to determine how Root should use its Stalk.

RSPs follow the same structure as RIPs, except that the length of the Voting Period can be reasonably shortened to ensure the will of Root DAO can be reflected in the governance process when appropriate.

## **Voting for RIPs**

Voting for RIPs will take place on Snapshot, using Root ownership at the time of proposal on Snapshot. Any Root holder can vote for or against any Snapshot proposal. In all instances, 1 Root equals 1 vote, and voting against a proposal is equivalent to abstaining.

A Voting Period begins when a vote for a RIP can be submitted to Snapshot and ends at approximately the beginning of the 168th Beanstalk Season after it begins, or when the RIP is committed with a supermajority.

If at the end of the Voting Period:

* Less than or equal to half of the total outstanding eligible Roots votes in favor of the RIP, it fails; and
* More than half of the total outstanding eligible Roots votes in favor of the RIP, it passes.&#x20;

If at any time before the end of the Voting Period more than two-thirds of the total outstanding eligible Root votes in favor of the RIP, it passes and the RDM can commit and execute the RIP on-chain.

## **RDM Best Practices**

RDM Signers shall follow the best practices outlined below. It is of paramount importance that Root limits key man risk by implementing best practices with respect to multisig custody. Signers are expected to:

1. Regularly check in with the RDM and confirm access to their wallet;&#x20;
2. Maintain active communication regarding travel plans and availability in order to ensure that there are always enough Signers on call; and
3. Acknowledge their Signer duties and processes for signing off on RIPs.

In addition to the above expectations, Signers shall follow the RDM's wallet security best practices:

1. Use a reputable hardware wallet like Trezor or Ledger;
2. Use a fresh wallet that doesn't have any pre-existing transactions or balances on it;
3. Set up a new passphrase on their hardware wallet device when selecting a new wallet to be the signing wallet; and
4. Follow the standard self-custody best practice guide [here](https://blog.trailofbits.com/2018/11/27/10-rules-for-the-secure-use-of-cryptocurrency-hardware-wallets/).

## **Signer Duties**

Signers are expected to follow best practices and maintain active communication in order to ensure that there are always enough Signers available to execute transactions in case of an emergency. Signer duties are broken down into three stages: 1) confirming access to their wallet, 2) verifying proposed code changes and 3) executing transactions on the RDM Gnosis wallet.

When a draft RIP is proposed, every Signer shall be notified of the timeline and shall confirm access to their wallet.

Once a RIP Snapshot is proposed, all Signers are expected to promptly review and verify that the proposed code changes are accurately represented. After a Signer has followed the guide laid out in the [#reviewing-and-signing-off-on-transactions](rdm-process.md#reviewing-and-signing-off-on-transactions "mention") section, they will submit and sign an etherscan message that publicly confirms their review. This will 1) limit blind signing and 2) encourage each Signer to verify that a RIP’s code changes are accurately represented and distributed to the public. The steps to create and verify a signature on etherscan can be found [here](https://info.etherscan.com/verify-signature-tool/). Anyone can verify that the Signer reviewed and signed off on the proposed code changes during the Voting Period.

Signers will sign the transaction to either execute the proposed transaction or cancel it as soon as possible following the conclusion of the Voting Period.

Once sufficient signatures have been provided to execute the transaction, is it expected that one of the Signers execute the transaction. Signers are not expected to contribute capital to participate in the RDM.

A Signer shall lose their role (by action of the remaining Signers removing them) in case they:

* Act against Root Token Holder’s off-chain voting;
* Do not follow best practices outlined in the [#rdm-best-practices](rdm-process.md#rdm-best-practices "mention") section; or
* Get through 2 months or 2 votes (whichever happens first) without performing any of their Signer duties.

## **Emergency Response Procedures**

The RDM’s role is to 1) enact on-chain the decisions Root Token Holders make via off-chain voting and 2) review and verify proposals to ensure the suggested changes are truthfully represented. However, if an emergency arises, like a bug or security vulnerability, it is of critical importance that the RDM takes swift action to protect Root.

**Depending on the severity of a given emergency, RDM members shall swiftly decide the best course of action:**

* If an emergency is severe and requires significant code changes to fix, the RDM will take any necessary extra action to mitigate further damage; or
* If an emergency is minor and does not require significant code changes, an emergency hotfix may be implemented by an emergency vote of the RDM.

Any changes made to Beanstalk in this manner are known as ERIPs, or Emergency RIPs.

**After emergency action is taken, the RDM shall swiftly issue a summarized report to the community detailing:**

1. The administrative permissions that were used (e.g. upgrading Root or turning off certain functions);
2. The context and severity of the issue; and&#x20;
3. The next steps and decisions, if any, that the community must agree on in order for Root to proceed.

#### **Reviewing and Signing off on Transactions**

Everyone on the RDM shall be expected to know how to verify `upgradeTo()` and `upgradeAndCallTo()` data and submit an etherscan transaction confirming they have checked the submitted transaction.

As a part of submitting RIPs, the proposer will be responsible for providing thorough documentation or supplementary video to Root DAO and RDM for how to review/test all relevant code. The following should be used as a guide for the minimum review criteria:

* Check function call is as expected
* Check calldata is correct&#x20;
* Test RIP on mainnet fork or testnet as necessary&#x20;
* Review conceptual changes involved in RIP&#x20;
* Review Github PR change log (naming or other small nits)&#x20;
* Review constants (contract addresses, numbers) in new contracts

Once Signers have verified the transaction, they shall submit and sign a [verified etherscan message](https://info.etherscan.com/verify-signature-tool/) and distribute the public verification link to the RDM.

{% hint style="warning" %}
Note: In cases where RSPs are simply voting in a governance process, the RDM signers are not expected to perform the full verification process required for RIPs.
{% endhint %}

#### **Problems During Verification**

The RDM will not submit a transaction that was misrepresented on Snapshot.

In the case that any Signer during the verification process determines that a GitHub PR does not accurately represent the RIP, that Signer will submit a verified etherscan message indicating as such with context on the issue. At that point, the RDM will not submit the transaction unless it is determined that the Signer is "rogue" and is attempting to censor the RIP. In the case the other Signers determine that one or more Signers is rogue, they will submit a verified etherscan message indicating as such. At that point all present key holders shall submit a new verified etherscan message to cancel the original transaction.

The RDM will notify the community via Discord and work with the proposer to resolve the issue in the GitHub PR. Once resolved, a new RIP will be proposed on Snapshot with its associated transaction.

## **Rotating Holders In / Out**

In the event that one or more Signers are compromised or vote against the results of any Snapshot (or a Signer voluntarily chooses to be removed from the RDM), the RDM will rotate them out of the wallet and replace them with another Signer. In no instance shall more than 3 keys be held by Root contributors, nor shall more than 1 key be held by Mistermanifold.

Once a transaction is submitted on-chain, the RDM will adhere to the results of the Snapshot and each member shall verify the transaction on etherscan during the Voting Period.

If a situation arises where not all Signers submit a verification, the RDM may continue with execution if the Signer:

1. Was not responsive during Snapshot proposal;&#x20;
2. Failed to notify the RDM during the draft phase of the proposal that they would not be able to execute the transaction;&#x20;
3. Missed 2 verifications;&#x20;
4. Was not responsive in 2 months; or&#x20;
5. Votes against the result of any Snapshot vote (AWOL). In this case, the Signer would be subject to removal immediately.

## **Anonymous Multisig Signers**

Off-chain governance introduces significant risks related to security and censorship. The RDM is designed to mitigate as many of those risks as possible by distributing the multisig keys across reputable community members and contributors to Root and Beanstalk, and collectively implementing and adhering to RDM best practices.

The most significant risk associated with off-chain governance is the potential corruption of the multisig wallet from an outside party. In order to minimize the chances of this, the Signers will be anonymous. The anonymous Signers will be selected by Mistermanifold. Signers will be anonymous to each other as well, apart from Mistermanifold.

A maximum of 3 Signers will be members of Root. Mistermanifold will hold at most 1 key. The remaining keys will be held by reputable members of the Root and Beanstalk community.
