---
description: WithdrawDOT
---

# Withdraw DOT

You can withdraw DOTs contributed to crowdloans that are expired, and stake them via Euphrates to earn DOT staking yield and boosted rewards. Below is a guide for withdraw and stake DOT.

### 1. **Withdraw DOT contributed to crowdloan via Polkadot{JS}**

When the lease periods won by the crowdloan have finished, or the crowdloan has ended without winning a slot, anyone can trigger the refund of crowdloan contributions back to their original owners.

This can be done through the permissionless `crowdloan.refund` extrinsic available on [Polkadot JS Apps](https://polkadot.js.org/apps) > Developer > Extrinsics page, by specifying the parachain ID. This extrinsic may need to be issued multiple times, if the list of contributors is too long. All contributions must be returned before the crowdloan is entirely deleted from the system.

Read more [here](https://wiki.polkadot.network/docs/learn-crowdloans#withdraw-crowdloaned-tokens)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### 2. **Bridge DOT to Acala**

2.1 Connect to [Acala Apps](https://apps.acala.network/) and click on `Bridge` on the left-hand side of the page.

Keep Polkadot as the `Origin Chain` and select Acala as the `Destination Chain`. Enter the amount of DOT you’d like to send. Click `Transfer`.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

2.2 Return to the Portfolio tab to see your transferred DOT balance.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 3. **Stake DOT to LDOT or tDOT pool**

You can stake DOT to earn DOT staking yield and boosted rewards in ACA and participating project tokens e.g. TAI. Following [this guide](https://farmdoc.acala.network/how-to-guides/use-euphrates/stake-dot) for staking DOT.
