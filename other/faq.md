# FAQ

### When can I convert my LCDOT back to DOT?

After the Acala crowdloan unlock ([at block 17856000, 00:08 UTC Oct 24\~](https://polkadot.subscan.io/block/17856000)).

### What is LCDOT?

LCDOT stands for Liquid Crowdloan DOT. It is a token that is a 1:1 representation of DOT locked in the Acala crowdloan. You can obtain LCDOT from [Acala Swap](https://apps.acala.network/swap).

### What is Euphrates?

Euphrates primarily allows stakers and liquidity providers of LSTs (liquid staking tokens) to earn boosted rewards and also claim ACA and other participating project token rewards. Euphrates will be deployed with DOT-based LST liquidity vaults, and later expanded to support Ethereum and other multichain LST liquidity vaults.

### How does Euphrates work?

For LCDOT stakers, DOT will automatically be claimed and turned into an LST of choice upon the Acala crowdloan unlock ensuring users don’t miss a day of DOT staking rewards.

For DOT stakers, DOT will automatically be turned into an LST of choice.

LSTs can be withdrawn at any time and both paths reward ACA and participating project tokens

### Is it safe to use and work with Euphrates?

In order to be safe, Euphrates continues to do the following

* Open sourcing & continuous reviewing of all codes
* Use non-custodial staking service to eliminate counter-party risks
* External audits can be found here

### What are the risks of using Euphrates?

There are always \*\*\*\*inherent risks associated with engaging with decentralized-finance smart contracts, pallets and networks :

* Smart Contract & Pallet risks: Euphrates code is open-sourced, audited and covered by bug bounty
* Associated risks from protocols including [Acala Liquid Crowdloan DOT LCDOT](https://wiki.acala.network/crowdloans/acala-crowdloan/faq#liquid-crowdloan-and-lcdot), [Homa Liquid Staking DOT](https://docs.homastaking.app/) and [Taiga Finance tDOT](https://www.taigaprotocol.io/) as Euphrates integrates directly with them.

Acala is determined to mitigate the above risks and eliminate them entirely to the extent possible. Despite this, they may still exist.

### What is staking APR for LCDOT?

There are two staking pools for LCDOT, LDOT pool and tDOT pool.

**Before unlock (aka Acala lease ends)**

LDOT Pool APR = ACA incentive APR

tDOT Pool APR = ACA incentive APR + TAI incentive APR

**After unlock (aka Acala lease ends)**

LDOT Pool APR = ACA incentive APR + LDOT APR

tDOT Pool APR = ACA incentive APR + TAI incentive APR + tDOT APR

Read more about rewards [here](../euphrates/rewards.md)

### What is staking APR for DOT?

There are two staking pools for DOT, LDOT pool and tDOT pool.

LDOT Pool APR = ACA incentive APR + LDOT APR

tDOT Pool APR = ACA incentive APR + TAI incentive APR + tDOT APR

Read more about rewards [here](../euphrates/rewards.md)

### What is tDOT?

tDOT is the synthetic stable asset that is backed by the DOT Stable Swap. You can read about the details of its architecture [here](https://docs.taigaprotocol.io/overview/architecture#tdot).

### What is LDOT?

LDOT is a staking yield-bearing token. It represents the principle staked DOT plus the staking yield continuously accruing. You can read more about L-Tokens [here](https://docs.homastaking.app/overview/l-token).

### How can I unstake?

Navigate to the pool that you have staked, then navigate to the 'Current Stake' section. Click on the 'Unstake' button to unstake your assets. For LCDOT, you can unstake the LSTs that LCDOT converts into after the unlock (parachain lease expires). Read more here.

### How can I withdraw DOT with my LCDOT?

If you do not want to participate in LCDOT staking, you can choose to withdraw DOT from crowdloan after the unlock. Withdraw DOT from LCDOT [here](https://farm.acala.network/withdraw)
