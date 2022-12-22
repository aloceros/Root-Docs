# Mechanics

Any Ethereum account can Mint and Redeem Roots for Beanstalk Silo Deposits on the Minting Whitelist through Root at anytime. Anytime Roots are Minted or Redeemed, the [BDV](https://docs.bean.money/almanac/protocol/glossary#bean-denominated-value), [Stalk](https://docs.bean.money/almanac/protocol/glossary#stalk) and [Seeds](https://docs.bean.money/almanac/protocol/glossary#seeds) per either remain the same or increase.&#x20;

All value in Root is owned pro rata by Root Holders. Any account can contribute to collective farming by calling the `earn`, `mow`, `updateBDV` and `updateBDVs` functions.

### Minting Whitelist

Any ERC-20 standard token that is on the [Beanstalk Deposit Whitelist](https://docs.bean.money/almanac/farm/silo#deposit-whitelist) can be added to and removed from the Minting Whitelist via Root governance.&#x20;

Any Beanstalk Silo Deposit of a token on the Minting Whitelist can be used to Mint Roots.

#### Current Minting Whitelist

| Whitelisted asset | Address                                                                                                               |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| Bean              | [0xBEA0000029AD1c77D3d5D23Ba2D8893dB9d1Efab](https://etherscan.io/address/0xBEA0000029AD1c77D3d5D23Ba2D8893dB9d1Efab) |

### Mint

To Mint Root, an account must call the `mint` function and provide a minimum amount of Root to Mint, and a list of Beanstalk Silo Deposits on the Minting Whitelist that are not currently owned by Root.

The amount of Root received will be the greater of the minimum amount of Root specified, or the minimum of the percentage change in the BDV, Stalk, or Seeds of Root resulting from the Mint, multiplied by the total Root supply.

### Redeem

To Redeem Root, an account must call the `redeem` function and provide a maximum amount of Root to Redeem, and a list of Beanstalk Silo Deposits currently owned by Root.

The amount of Root needed to Redeem a list of Beanstalk Silo Deposits is the lesser of the amount specified, or the maximum of the percentage change in the BDV, Stalk, or Seeds of Root resulting from the Redemption, multiplied by the total Root supply.

### Earn

The `earn` function can be called by any account to [Mow](https://docs.bean.money/almanac/protocol/glossary#mow) all of Root’s [Grown Stalk](https://docs.bean.money/almanac/protocol/glossary#grown-stalk), [Plant](https://docs.bean.money/almanac/protocol/glossary#plant) the Seeds associated with Root’s [Earned Beans](https://docs.bean.money/almanac/protocol/glossary#earned-beans) and Deposit Root’s Earned Beans in the current [Season](https://docs.bean.money/almanac/protocol/glossary#season).

This is the only instance the Stalk or Seed per BDV ratios of Root may decrease.

### Mow

The `mow` function can be called by any account to Mow all of Root’s Grown Stalk.

### Update BDV

Any account can update the BDV of one or multiple of Root’s Silo Deposits by calling the `updateBdv` or `updateBdvs` functions, respectively.
