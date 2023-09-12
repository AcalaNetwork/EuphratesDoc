# UpgradeableStakingLST

* [Source code](https://github.com/AcalaNetwork/Euphrates)
* Deployed contract

### **Staking-related Methods**

#### stake()

Staking share into staking pool.

```solidity
function stake(uint256 poolId, uint256 amount) external nonpayable returns (bool)
```

| Parameter | Type    | Description                    |
| --------- | ------- | ------------------------------ |
| poolId    | uint256 | The index of staking pool.     |
| amount    | uint256 | The share amount to be staked. |

#### unstake()

Withdraw share from staking pool.

```solidity
function unstake(uint256 poolId, uint256 amount) external nonpayable returns (bool)
```

| Parameter | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| poolId    | uint256 | The index of staking pool.       |
| amount    | uint256 | The share amount to be un-staked |

\<aside> \<img src="/icons/info-alternate\_gray.svg" alt="/icons/info-alternate\_gray.svg" width="40px" /> If the pool has been converted, the withdrawn token should be the converted token. If the converted token is WTDOT, the retrieved token should be tDOT.

\</aside>

#### claimRewards()

Claim all rewards from staking pool.

```solidity
function claimRewards(uint256 poolId) external nonpayable returns (bool)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The index of staking pool. |

#### exit()

Un-stake all staked share and claim all unclaimed rewards from staking pool.

```solidity
function exit(uint256 poolId) external nonpayable returns (bool)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The index of staking pool. |

\<aside> \<img src="/icons/info-alternate\_gray.svg" alt="/icons/info-alternate\_gray.svg" width="40px" /> It is the order to execute `unstake` + `claimRewards`, if any event is banned, it will be reverted。

\</aside>

### Pool config-related Methods

#### **poolIndex**()

Get the index of next [pool.It](http://pool.it)’s equal to the current count of pools. This is zero by default.

```solidity
function poolIndex() external view returns (uint256)
```

\<aside> \<img src="/icons/info-alternate\_gray.svg" alt="/icons/info-alternate\_gray.svg" width="40px" /> This value will be incremented by 1 whenever `addPool`.

\</aside>

#### addPool()

Initialize a staking pool for `shareType`.

Can be called only by owner.

```solidity
function addPool(contract IERC20 shareType) external nonpayable
```

| Parameter | Type            | Description                                       |
| --------- | --------------- | ------------------------------------------------- |
| shareType | contract IERC20 | Initialize the ERC20 contract address of the pool |

#### **updateRewardRule()**

Update the reward rule of `rewardType` for `poolId` pool.

Can be called only by owner.

```solidity
function updateRewardRule(
	uint256 poolId, 
	contract IERC20 rewardType, 
	uint256 rewardRate, 
	uint256 endTime
) external nonpayable
```

| Parameter  | Type            | Description                   |
| ---------- | --------------- | ----------------------------- |
| poolId     | uint256         | The index of staking pool.    |
| shareType  | contract IERC20 | The reward token address.     |
| rewardRate | uint256         | The reward amount per second. |
| endTime    | uint256         | The end time of rule.         |

#### **rewardRules**()

Get the reward rule for `rewardType` reward of `poolId` pool.

```solidity
function rewardRules(uint256 poolId, contract IERC20 rewardType) external view returns (struct Staking.RewardRule)

struct RewardRule {
    // Reward amount per second.
    uint256 rewardRate;
    // The end time for reward accumulation.
    uint256 endTime;
    // Accumulated reward rate, this is used to calculate the reward amount of each staker.
    // It mul 1e18 to avoid loss of precision.
    uint256 rewardRateAccumulated;
    // The last time of this rule accumulates reward.
    uint256 lastAccumulatedTime;
}
```

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| rewardType | contract IERC20 | The reward token address.  |

#### **setRewardsDeductionRate()**

Set deduction `rate` of claim rewards for `poolId` pool.

Can be called only by owner.

```solidity
function setRewardsDeductionRate(uint256 poolId, uint256 rate) external nonpayable
```

| Parameter | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| poolId    | uint256 | The index of staking pool.       |
| rate      | uint256 | The deduction rate. 1e18 is 100% |

#### **rewardsDeductionRates**()

Get the rewards deduction rate of `poolId` pool.

```solidity
function rewardsDeductionRates(uint256 poolId) external view returns (uint256)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The index of staking pool. |

\<aside> \<img src="/icons/info-alternate\_gray.svg" alt="/icons/info-alternate\_gray.svg" width="40px" /> The deduction rate. 1e18 is 100%

\</aside>

#### **shareTypes**()

Get the share token of `poolId` pool.

```solidity
function shareTypes(uint256 poolId) external view returns (contract IERC20)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The pool id to be queried. |

#### **shares**()

Get the share amount of `who` of `poolId` pool.

```solidity
function shares(uint256 poolId, address who) external view returns (uint256)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The pool id to be queried. |
| who       | address | The address of staker.     |

#### **totalShares**()

Get the total share amount of `poolId` pool.

```solidity
function totalShares(uint256 poolId) external view returns (uint256)
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The pool id to be queried. |

#### **earned**()

Get `who`'s unclaimed reward amount of specific `rewardType` at `poolId` pool.

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| who        | address         | The address of staker.     |
| rewardType | contract IERC20 | The reward token address.  |

#### **rewardPerShare**()

Get the exchange rate for share to `rewardType` reward token of `poolId` pool.

_The reward part is accumulated rate adds pending to accumulate rate, it's used to calculate reward. 1e18 is 100%._

```solidity
function rewardPerShare(uint256 poolId, contract IERC20 rewardType) external view returns (uint256)
```

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| rewardType | contract IERC20 | The reward token address.  |

#### **rewardTypes**()

Get the reward token types of `poolId` pool.

```solidity
function rewardTypes(uint256 poolId) external view returns (contract IERC20[])
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The index of staking pool. |

#### **rewards**()

Get the unclaimed paid `rewardType` reward amount for `who` of `poolId` pool.

```solidity
function rewards(uint256 poolId, address who, contract IERC20 rewardType) external view returns (uint256)
```

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| who        | address         | The address of staker.     |
| rewardType | contract IERC20 | The reward token address.  |

#### **lastTimeRewardApplicable**()

Get latest time that can be used to accumulate rewards for `rewardType` reward of `poolId` pool.

```solidity
function lastTimeRewardApplicable(uint256 poolId, contract IERC20 rewardType) external view returns (uint256)
```

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| rewardType | contract IERC20 | The reward token address.  |

#### **paidAccumulatedRates**()

Get the paid accumulated rate of `rewardType` for `who` of `poolId` pool.

```solidity
	function paidAccumulatedRates(uint256 poolId, address who, contract IERC20 rewardType) external view returns (uint256)
```

| Parameter  | Type            | Description                |
| ---------- | --------------- | -------------------------- |
| poolId     | uint256         | The index of staking pool. |
| who        | address         | The address of staker.     |
| rewardType | contract IERC20 | The reward token address.  |

### Pool conversion-related Methods

#### **convertLSTPool()**

convert the share token of ‘poolId’ pool to LST token by `convertType`.

```solidity
function convertLSTPool(uint256 poolId, enum UpgradeableStakingLST.ConvertType convertType) external nonpayable

enum ConvertType {
		LCDOT2LDOT,
    LCDOT2TDOT,
    DOT2LDOT,
    DOT2TDOT,
    LCDOT2WTDOT,
    DOT2WTDOT
}
```

| Parameter   | Type                                   | Description                |
| ----------- | -------------------------------------- | -------------------------- |
| poolId      | uint256                                | The index of staking pool. |
| convertType | enum UpgradeableStakingLST.ConvertType | The convert type.          |

#### **convertInfos**()

Get the LST conversion info of `poolId` pool.

```solidity
function convertInfos(uint256 poolId) external view returns (struct UpgradeableStakingLST.ConvertInfo)

struct ConvertInfo {
    // The converted LST token.
    IERC20 convertedShareType;
    // This is a snapshot of the ratio between share amount to new share token amount at the moment of conversion. 1e18 is 1:1
    uint256 convertedExchangeRate;
}
```

| Parameter | Type    | Description                |
| --------- | ------- | -------------------------- |
| poolId    | uint256 | The index of staking pool. |

\<aside> \<img src="/icons/info-alternate\_gray.svg" alt="/icons/info-alternate\_gray.svg" width="40px" /> If the pool has been converted, the withdrawn token should be the converted token. If the converted token is WTDOT, the retrieved token should be tDOT.

\</aside>

### Pool operation pause-related Methods

#### **setPoolOperationPause()**

Set the `paused` status of `operation` for `poolId` pool.

Can be called only by owner.

```solidity
function setPoolOperationPause(
	uint256 poolId, 
	enum PoolOperationPausable.Operation operation, 
	bool paused
) external nonpayable

enum Operation {
    Stake,
    Unstake,
    ClaimRewards
}
```

| Parameter | Type                                           | Description                |
| --------- | ---------------------------------------------- | -------------------------- |
| poolId    | uint256                                        | The index of staking pool. |
| operation | enum PoolOperationPausable.Operation operation | The user operation.        |
| paused    | bool                                           | The pause status.          |

#### **pausedPoolOperations**()

Get the pause status of `operation` for `poolId` pool.

```solidity
function pausedPoolOperations(uint256 poolId, enum PoolOperationPausable.Operation operation) external view returns (bool)

enum Operation {
    Stake,
    Unstake,
    ClaimRewards
}
```

| Parameter | Type                                           | Description                |
| --------- | ---------------------------------------------- | -------------------------- |
| poolId    | uint256                                        | The index of staking pool. |
| operation | enum PoolOperationPausable.Operation operation | The user operation.        |

### Contract config-related Methods

#### owner()

Get the owner of the contract.

```solidity
function owner() external view returns (address)
```

#### DOT()

Get the bound DOT token address

```solidity
function DOT() external view returns (address)
```

#### **HOMA**()

Get the bound HOMA token address

```solidity
	function HOMA() external view returns (address)
```

#### **LCDOT**()

Get the bound LCDOT token address

```solidity
function LCDOT() external view returns (address)
```

#### LDOT()

Get the bound LDOT token address

```solidity
function LDOT() external view returns (address)
```

#### LIQUID\_CROWDLOAN()

Get the bound LiquidCrowdloan pre-deploy contract address

```solidity
function LIQUID_CROWDLOAN() external view returns (address)
```

#### **MAX\_REWARD\_TYPES**()

The maximum number of reward types for a staking pool. When distribute and receiving rewards, all reward types of a pool will be iterated. Limit the number of reward types to avoid out of huge gas.

```solidity
function MAX_REWARD_TYPES() external view returns (uint256)
```

#### **STABLE\_ASSET**()

Get the bound StableAsset pre-deploy contract address

```solidity
function STABLE_ASSET() external view returns (address)
```

#### **TDOT**()

Get the bound tDOT token address

```solidity
function TDOT() external view returns (address)
```

#### **pause()**

Pause the contract.

Can be called only by owner.

```solidity
function pause() external nonpayable
```

#### **unpause()**

Unpause the contract.

Can be called only by owner.

```solidity
function unpause() external nonpayable
```

#### **paused**()

Returns true if the contract is paused, and false otherwise.

```solidity
function paused() external view returns (bool)
```

#### **transferOwnership()**

Transfers ownership of the contract to a new account (`newOwner`). Can only be called by the current owner.

Can be called only by owner.

```solidity
function transferOwnership(address newOwner) external nonpayable
```

| Parameter | Type    | Description               |
| --------- | ------- | ------------------------- |
| newOwner  | address | The address of new owner. |

#### **renounceOwnership()**

Leaves the contract without owner. It will not be possible to call `onlyOwner` functions. Can only be called by the current owner. NOTE: Renouncing ownership will leave the contract without an owner, thereby disabling any functionality that is only available to the owner.

Can be called only by owner.
