# RDM Process

{% hint style="info" %}
In an attempt to facilitate a secure and transparent multisig process, the Root DAO Multisig (RDM) follows similar processes followed by the [Beanstalk Community Multisig](https://docs.bean.money/almanac/governance/beanstalk/bcm-process).
{% endhint %}

The RDM has the exclusive and unilateral ability to submit and commit RIPs, and vote on BIPs. The RDM is a [Safe](https://safe.global/) multisig wallet with anonymous signers consisting of community members and contributors to Root and Beanstalk. Its m-of-n configuration will start as 4-of-7 on Ethereum mainnet. Parameters m and n are each ultimately defined by Root Holders and may evolve in the future via RIP.

Voting for RIPs takes place on Snapshot using **Voting Roots**, defined as the minimum of each account's Roots between the beginning and end of the Voting Period.

The RDM will provide sufficient notice of the submission of a RIP, its contents and the beginning of its Voting Period before submitting a RIP to Snapshot, and will repost BIPs on the [Root Stalk Proposals Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) as soon as possible after they are posted to the [Beanstalk DAO Snapshot page](https://snapshot.org/#/beanstalkdao.eth).

* [Multisig Powers](rdm-process.md#multisig-powers)
* [Snapshot Usage](rdm-process.md#snapshot-usage)
* [RIP Proposal and Voting](rdm-process.md#rip-proposal-and-voting)
* [RSP Proposal and Voting](rdm-process.md#rsp-proposal-and-voting)
* [Signer Best Practices](rdm-process.md#signer-best-practices)
* [Signer Duties](rdm-process.md#signer-duties)
* [Verifying and Signing Transactions](rdm-process.md#verifying-and-signing-transactions)
* [Emergency Response Procedures](rdm-process.md#emergency-response-procedures)
* [Rotating Signers](rdm-process.md#rotating-signers)
* [Anonymous Signers](rdm-process.md#anonymous-signers)

## **Multisig Powers**

Root is an upgradable contract that uses [OpenZeppelin's UUPS](https://docs.openzeppelin.com/contracts/4.x/api/proxy#UUPSUpgradeable) implementation.

The mechanism for upgrading Root is by calling either `upgradeTo`, which takes an argument of the new implementation address, or `upgradeToAndCall`, which takes arguments of a new implementation address and an optional function call. The `upgradeTo` and `upgradeToAndCall` functions are only callable by the owner of Root, which is the RDM.

Upgrades should only be executed after a RIP has passed and Signers have manually reviewed the code changes. However, in the case of an emergency (like a bug or vulnerability), the RDM may execute transactions to protect the Root contract. The best practices for emergency response handling are outlined in the [#emergency-response-procedures](rdm-process.md#emergency-response-procedures "mention") section.

If a Root Holder wants to propose a RIP, they can submit a pull request to the [Root Github repo](https://github.com/RootToken) and begin a formal process with the RTM outlined in the [#rip-proposal-process](rdm-process.md#rip-proposal-process "mention") section.

The following functions are only callable from the owner address:

* `upgradeTo` — Upgrade the Root token contract to a new implementation address.
* `upgradeToAndCall` — Upgrade Root token contract to a new implementation address and/or execute and `init` function with a `delegatecall`.
* `transferOwnership` — Nominate a candidate to become the new owner of the Root token contract. The newly nominated candidate will then need to call `claimOwnership` before ownership of the contract is transferred.
* `renounceOwnership` — This function is currently disabled so calling it will revert. The function is still there because the ownership contract is inherited from OpenZeppelin.
* `addWhitelistToken` — Add a token to the Minting Whitelist.
* `removeWhitelistToken` — Remove a token from the Minting Whitelist.
* `setDelegate` — Delegate Snapshot Stalk voting power of the Root contract.

## **Snapshot Usage**

The RDM is an extension of Root DAO. As such, the RDM's role is to (1) enact on-chain the decisions Root holders make via off-chain voting and (2) review and verify proposals to ensure the suggested changes are truthfully represented.

RIPs are voted on at the [Root DAO Snapshot page](https://snapshot.org/#/rootsmoney.eth).

The RDM shall not execute transactions until an associated Snapshot proposal successfully passes, apart from the exceptions outlined in the table below:

| Transaction                                          | Snapshot                                         | Voting Period                                                                                      |
| ---------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Executing RIP                                        | Yes, requires a passed RIP                       | Up to 168 Beanstalk Seasons as outlined in [#rip-voting](rdm-process.md#rip-voting "mention")      |
| Non-emergency change to the m-of-n RDM configuration | Yes, requires a passed RIP                       | Up to 168 Beanstalk Seasons as outlined in [#rip-voting](rdm-process.md#rip-voting "mention")      |
| Executing RSP                                        | Yes, requires a passed RSP                       | Up to 168 Beanstalk Seasons as outlined in the [#rsp-voting](rdm-process.md#rsp-voting "mention")  |
| Executing ERIP (emergency hotfix, etc.)              | No, but requires public notification via Discord | N/A                                                                                                |
| Rotating RDM Signers                                 | No                                               | N/A                                                                                                |
| Emergency change to the m-of-n RDM configuration     | No                                               | N/A                                                                                                |
| Cancel Transaction                                   | No                                               | N/A                                                                                                |

## RIP Proposal and Voting

Root governance is modeled after Beanstalk governance. Root governance is designed to be as permissionless as possible. Any Root Holder with 0.1% of total Roots may propose RIPs. If a Root Holder wishes to propose a RIP they must complete a public proposal process before the RDM will submit a Snapshot proposal and an on-chain transaction to the RDM on their behalf.

### RIP Proposal Content

RIPs can propose to (1) change the Root token or (2) change Root governance. RIPs consist of a pull request on the Root GitHub repo that includes the following\*:

* Code implementing the proposed changes;
* A written proposal of the changes that would be implemented in the RIP, which must include:
  * A **Proposer** section that includes a [verified Etherscan message](https://info.etherscan.com/verify-signature-tool/) confirming the proposer address of the given RIP (note that the address must also have at least 0.1% of total Voting Roots at the end of the Voting Period); and
  * Information about the on-chain transaction that the RDM should submit, i.e., the function name and input parameters.

\*In cases where a RIP has no associated implementation, a pull request only needs to propose changes to the [`proposals.md`](https://github.com/RootToken/Root/blob/master/proposals.md) file.

RIPs may have multiple transactions if made explicit in the written proposal.&#x20;

### RIP Proposal Process

The following are the processes in place for a Root Holder to propose a RIP:

* Submit a pull request on the public Root GitHub repo with a written proposal of the changes that would be implemented in the RIP.
* Tag the **@RDM Liaison** user in the **(#🌳・canopy)** channel in the Root Discord to create a dedicated discussion channel for the RIP.
* Share a link to the GitHub PR and the written proposal in the newly created dedicated discussion channel.
* Allow sufficient time for discussion of the proposal. What constitutes sufficient is at the sole discretion of the RDM, but the RDM must formally propose the RIP within 2 weeks of the creation of the dedicated discussion channel, unless the proposer decides to withdraw their proposal.
* Tag the **@RDM Liaison** user to request that the BIP be formally proposed.
* Before the RDM formally proposes the RIP, they shall verify that the written proposal contains all the necessary content per [#rip-proposal-content](rdm-process.md#rip-proposal-content "mention").
* The RDM shall then formally propose the RIP by submitting the on-chain transaction and Snapshot proposal.
* During the Voting Period (1-7 days), every RDM Signer shall verify the transaction per [#verifying-and-signing-transactions](rdm-process.md#verifying-and-signing-transactions "mention"). If not all Signers verify the transaction, the RDM may still continue per the process outlined in [#rotating-signers](rdm-process.md#rotating-signers "mention").
* If the RIP passes, the Signers will sign m/n signatures and execute the on-chain transaction as soon as possible. If the RIP fails to pass, the Signers will submit and execute a cancel transaction with the same nonce as soon as possible.

### RIP Voting

Voting for RIPs takes place on Snapshot using **Voting Roots**, defined as the minimum of each account's Roots between the beginning and end of the Voting Period.

Any Root Holder can vote For or Abstain on any RIP. In all instances, 1 Root equals 1 vote, and not voting or voting Abstain is equivalent to voting against.

The Voting Period opens when the Snapshot proposal for a RIP can be voted on and ends at approximately the beginning of the 168th Beanstalk Season after it begins, or when the RIP is committed with a supermajority.

If at the end of the Voting Period:

* Less than or equal to half of total Voting Roots votes in favor of the RIP, it fails, or
* More than half of total Voting Roots votes in favor of the RIP, it passes.

If at any time 24 hours or more after the beginning and before the end of the Voting Period more than two-thirds of total Voting Roots votes in favor of the RIP, the RDM can execute the RIP on-chain.

## RSP Proposal and Voting

In its capacity as a Stalkholder, Root ([0x7770...9a26](https://etherscan.io/address/0x77700005BEA4DE0A78b956517f099260C2CA9a26)) is entitled to vote on (1) each BIP and (2) other, non-BIP, governance processes, and may be entitled to non-Beanstalk-native yields.

Root Stalk Proposals (RSPs) are proposals for the Root DAO to determine how Root should use its Stalk in each governance process, and distribute yield, if ever.

In particular, any BIP automatically qualifies be proposed to Root DAO as a RSP. The RDM will repost BIPs on the [Root Stalk Proposals Snapshot page](https://snapshot.org/#/rootstalkproposals.eth) as soon as possible after they are posted to the [Beanstalk DAO Snapshot](https://snapshot.org/#/beanstalkdao.eth/) page. The RDM will vote on each BIP as determined by the RSP.

For other governance processes, a Root Holder must complete a public proposal process before the RDM will submit a Snapshot proposal on their behalf.

### RSP Proposal Content

RSPs consist of a pull request on the Root GitHub repo that includes the following:

* Updates to the [`proposals.md`](https://github.com/BeanstalkFarms/Beanstalk/blob/master/proposals.md) file;
* A written proposal of the way in which the Root DAO should use its Stalk, which must include:
  * A **Proposer** section that includes a [verified Etherscan message](https://info.etherscan.com/verify-signature-tool/) confirming the proposer address of the given RIP; and
  * Information about the on-chain transaction that the RDM should submit, i.e., the function name and input parameters (if applicable).

### RSP Proposal Process

The following are the processes in place for a Root Holder to propose a RSP that does not correspond to a BIP:

* Submit a pull request on the public Root GitHub repo with a written proposal per [#rsp-proposal-content](rdm-process.md#rsp-proposal-content "mention").
* Tag the **@RDM Liaison** user in the **(#🌳・canopy)** channel in the Root Discord to create a dedicated discussion channel for the RSP.
* Share a link to the GitHub PR and the written proposal in the newly created dedicated discussion channel.
* Allow sufficient time for discussion of the proposal. What constitutes sufficient is at the sole discretion of the RDM, but the RDM must formally propose the RSP within 2 weeks of the creation of the dedicated discussion channel, unless the proposer decides to withdraw their proposal.
* Tag the **@RDM Liaison** user to request that the RSP be formally proposed.
* Before the RDM formally proposes the RSP, they shall verify that the written proposal contains all the necessary content per [#rsp-proposal-content](rdm-process.md#rsp-proposal-content "mention").
* The RDM shall then formally propose the RSP by submitting the on-chain transaction (if applicable) and Snapshot proposal.
* During the Voting Period, every RDM Signer shall verify the transaction per [#verifying-and-signing-transactions](rdm-process.md#verifying-and-signing-transactions "mention"). If not all Signers verify the transaction, the RDM may still continue per the process outlined in [#rotating-signers](rdm-process.md#rotating-signers "mention").
* If the RSP passes, the Signers will sign m/n signatures and execute the on-chain transaction as soon as possible. If the RSP fails to pass, the Signers will submit and execute a cancel transaction with the same nonce as soon as possible.

### RSP Voting

RSPs follow the same structure as RIPs ([#rip-voting](rdm-process.md#rip-voting "mention")), except that the length of the Voting Period can be reasonably shortened to ensure the will of Root DAO can be reflected in the governance process when appropriate.

## **Signer Best Practices**

RDM Signers shall follow the best practices outlined below. It is of paramount importance that Root limits key man risk by implementing best practices with respect to multisig custody. Signers are expected to:

1. Regularly check in with the RDM and confirm access to their wallet;
2. Maintain active communication regarding travel plans and availability in order to ensure that there are always enough Signers on call; and
3. Acknowledge their Signer duties and processes for signing off on RIPs.

In addition to the above expectations, Signers shall follow the RDM's wallet security best practices:

1. Use a reputable hardware wallet like Trezor or Ledger;
2. Use a fresh wallet that doesn't have any pre-existing transactions or balances on it;
3. Set up a new passphrase on their hardware wallet device when selecting a new wallet to be the signing wallet; and
4. Follow the standard self-custody best practice guide [here](https://blog.trailofbits.com/2018/11/27/10-rules-for-the-secure-use-of-cryptocurrency-hardware-wallets/).

## **Signer Duties**

Signers are expected to follow best practices and maintain active communication in order to ensure that there are always enough Signers available to execute transactions in case of an emergency. Signer duties are broken down into three stages: (1) confirming access to their wallet, (2) verifying proposed transactions and (3) executing transactions on the RDM.

Once the Voting Period for a proposal begins on Snapshot, all Signers are expected to promptly review and verify that the proposed transaction accurately reflects the Snapshot proposal per [#verifying-and-signing-transactions](rdm-process.md#verifying-and-signing-transactions "mention"), if applicable. This limits blind signing and encourages each Signer to independently verify that a proposed transaction is accurately represented.

As soon as possible after the Voting Period:

* If the proposal passed, Signers who have verified the transaction will sign and execute the transaction; or
* If the proposal failed, Signers with sign and execute a cancel transaction with the same nonce.

A Signer shall lose their role on the RDM (by the remaining Signers removing them) if they:

* Act against Root Holders' off-chain voting;
* Do not follow best practices outlined in the [#signer-best-practices](rdm-process.md#signer-best-practices "mention") section; or
* Get through 2 months or 2 votes (whichever happens first) without performing any of their Signer duties.

## Verifying and Signing Transactions

All RDM Signers are expected to know how to verify `upgradeTo` and `upgradeAndCallTo` data and confirm they have verified transactions by signing a [verified Etherscan message](https://info.etherscan.com/verify-signature-tool/).

The following should be used as a guide for the minimum review criteria in cases where a  `upgradeTo` or `upgradeAndCallTo` is being executed:

* Perform the `upgradeTo` or `upgradeAndCallTo` on a local mainnet fork and confirm that the function call is as expected;
* Check that the `calldata` is correct;
* Confirm that the Root supply at the beginning of the Voting Period had not been corrupted by a flash loan, multi-block MEV or another governance attack;
* Review the GitHub PR code changes; and
* Review any audit reports, if applicable.

Once Signers have verified the transaction, they shall sign a [verified Etherscan message](https://info.etherscan.com/verify-signature-tool/) indicating that they have verified the transaction and share the link with the rest of the RDM.

This process must be completed for each transaction in a RIP.

If a situation arises where not all Signers submit a verification, the RDM may continue with execution if the Signer:

1. Was not responsive during the draft phase of the proposal or Voting Period;
2. Notified the rest of the RDM during the draft phase of the proposal that they would not be able to verify, sign or execute the transaction;
3. Missed 2 verifications;
4. Was not responsive in 2 months; or
5. Votes against the outcome of any proposal, in which case the Signer would be subject to removal immediately.

### **Problems During Verification**

The RDM will not submit a transaction that was misrepresented in the Snapshot proposal.

In the case that any Signer during the verification process determines that a Snapshot proposal does not accurately represent the transaction, that Signer will sign a message indicating as such with context on the issue and share it with the rest of the RDM.

The RDM will respond as follows:&#x20;

* If the RDM determines that the Signer is "rogue" and attempting to censor the transaction, the RDM will indicate that by continuing to verify (and ultimately sign, in the case that the proposal passes) the transaction; or
* If the RDM determines that the Signer is not rogue, the RDM will indicate that by submitting and signing a cancel transaction with the same nonce.

In cases where the RDM cancels a transaction, the community will be notified via the Root Discord and the RDM will work with the proposer to resolve the issue. Once resolved, a new proposal will be proposed on Snapshot with its associated transaction.

## **Emergency Response Procedures**

Although the RDM role is to enact on-chain the decisions Root Holders make via off-chain voting, it is of critical importance that the RDM take swift action to protect Root in the event of a bug or vulnerability. Emergency upgrades to Root submitted by the RDM are known as ERIPs.

Past ERIPs can be found [here](https://github.com/RootToken/Root-Governance-Proposals/blob/main/rip/erip).

Depending on the severity of a given emergency, RDM members shall swiftly decide the best course of action:

* If a bug or vulnerability is severe and requires significant code changes to fix, the RDM will take any necessary action to mitigate damage; or
* If a bug or vulnerability is minor and does not require significant code changes to fix, a hotfix may be implemented by the RDM.&#x20;

In cases where an immediate upgrade is necessary to protect Root, RDM Signers are not required to sign a verified Etherscan message as outlined in [#verifying-and-signing-transactions](rdm-process.md#verifying-and-signing-transactions "mention").

After emergency action is taken, the RDM shall swiftly issue a summarized report to the community via the Beanstalk Discord detailing:

1. The administrative permissions that were used;
2. The context and severity of the issue; and
3. The next steps and decisions, if any, that the community must agree on in order to proceed.

### ERIP During Voting Period

In the event that an ERIP must be executed during the Voting Period of another proposal, the on-chain transaction for the outstanding proposal must be canceled.&#x20;

In order avoid the need to revote on a proposal in this situation, the RDM will repropose the on-chain transaction for the outstanding proposal after the successful execution of the ERIP.

## **Rotating Signers**

In the event that one or more Signers are compromised or vote against the outcome of any proposal, voluntarily choose to be removed from the RDM, or are otherwise removed in accordance with [#signer-duties](rdm-process.md#signer-duties "mention"), the RDM will rotate them out of the multisig and replace them with another Signer. In no instance shall the majority of the RDM keys be held by active contributors to Root, nor shall more than 1 key be held by the creator of Root that selected the anonymous Signers.

## **Anonymous Signers**

Off-chain governance introduces significant risks related to security and censorship. The RDM is designed to mitigate as many of those risks as possible by distributing the multisig keys across reputable community members and contributors to Root and Beanstalk, and collectively implementing and adhering to [#signer-best-practices](rdm-process.md#signer-best-practices "mention").

The most significant risk associated with off-chain governance is the potential corruption of the multisig wallet from an outside party. In order to minimize the chances of this, the Signers are anonymous. The anonymous Signers are selected by one of the creators of Root. Signers are anonymous to each other as well, apart from the creator of Root who selected the Signers.

A maximum of 3 Signers are active contributors to Root. The remaining keys are held by reputable members of the Root and Beanstalk community.
