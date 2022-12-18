# Overview

## Background

Beanstalk's [credit based stability model](https://docs.bean.money/almanac/introduction/how-beanstalk-works) is a potential solution to the stablecoin carrying cost problem plaguing DeFi. Whereas other stablecoin protocols rely on collateral to issue stablecoins, which creates [centralization and carrying costs](https://docs.bean.money/almanac/introduction/why-beanstalk), Beanstalk uses infinitely scalable decentralized credit to create a permissionless stablecoin, Bean, that has carrying costs competitive with off-chain fiat.

Beanstalk does not offer [convertibility](https://docs.bean.money/almanac/advanced/stablecoin-overview#convertibility) and therefore does not maintain a perfect peg, Bean Depositors receive positive-carry in the form of Bean seigniorage in exchange for accepting some price volatility. Historically, blockchain-based businesses have not been able to compete with off-chain businesses because of non-competitive carry costs for low-volatility blockchain-native assets. The transparent distribution of Bean seigniorage to users flips this dynamic on its head, enabling blockchain-based businesses to finally compete with off-chain businesses.

While Bean is an ERC-20 standard token, in order to receive Beanstalk-native passive interest, Beans must be Deposited in the Silo, directly or wrapped in whitelisted LP tokens. However, Silo Deposits have two qualities that make them non-fungible: the [Stalk and Seeds per Bean Denominated Value (BDV)](https://docs.bean.money/almanac/farm/silo#deposit-whitelist) of each Deposit. The non-fungibility of Silo Deposits appears necessary to Beanstalk’s peg maintenance mechanism, but comes at the cost of composability.

## Root

Root is an Ethereum-native permissionless wrapper that implements the ERC-20 token standard to create fungibility and composability for Beanstalk Silo Deposits.

Root Holders share all value earned by Root pro rata across all Roots. The pro rata distribution creates a zero-fee shared collective farming option for passive Beanstalk Silo Depositors that (1) maximizes Beanstalk-native yield and (2) generates additional yield without creating significant risks to Beanstalk or Root.

Root is designed as a rent-free public good that can support many types of permissionless markets. Rent comes not only in the form of non-zero platform fees, but also in the requirement to use money with negative-carry costs. Instead of rent-based markets, markets denominated in Roots facilitate a new zero-fee, positive-carry market structure.&#x20;

For instance, users may agree to take opposing sides of a bet on the winner of the Super Bowl, and by denominated the bet in Roots, continue to earn interest on their positions before settlement. With Beanstalk-native yield, Root markets can structurally outcompete many traditional markets (for instance, pricing a more competitive line than Vegas).

Additional resources:

* [Root: Liquid, On-Chain Markets](https://medium.com/@rootmarkets/root-protocol-rent-free-markets-on-beanstalk-6a6b3f71415d)
