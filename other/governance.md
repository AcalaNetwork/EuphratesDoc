# Governance

The owner of `ProxyAdmin` contract controls `TransparentUpgradeableProxy` upgrade. The owner of `TransparentUpgradeableProxy` has the authority to configure the parameters of Euphrates and pause/unpuase the whole `TransparentUpgradeableProxy` contract.&#x20;

Euphrates smart contract is integrated with Acala on-chain governance, where management of Euphrates such as initializing pools, and adjusting incentive rewards are under the jurisdiction of on-chain governance. With caution and prudence of this new innovation (governance of smart contract via Acala/Substrate on-chain governance), there is a multi-sig setup managed by the Acala Foundation, to pause the contracts in case of emergency. This may also be replaced by on-chain governance as we progress.

## Governance Methods

### addPool

```solidity
function addPool(contract IERC20 shareType) external nonpayable
```

Initialize a staking pool for `shareType`.

#### Parameters

| Name      | Type            | Description      |
| --------- | --------------- | ---------------- |
| shareType | contract IERC20 | The share token. |

### claimRewards

```solidity
function claimRewards(uint256 poolId) external nonpayable returns (bool)
```

Claim all rewards from staking pool.

#### Parameters

| Name   | Type    | Description                |
| ------ | ------- | -------------------------- |
| poolId | uint256 | The index of staking pool. |

### convertLSTPool

```solidity
function convertLSTPool(uint256 poolId, enum UpgradeableStakingLST.ConvertType convertType) external nonpayable
```

convert the share token of ‘poolId’ pool to LST token by `convertType`.

#### Parameters

| Name        | Type                                   | Description                |
| ----------- | -------------------------------------- | -------------------------- |
| poolId      | uint256                                | The index of staking pool. |
| convertType | enum UpgradeableStakingLST.ConvertType | The convert type.          |

### pause

```solidity
function pause() external nonpayable
```

Puase the contract by Pausable.

### setPoolOperationPause

```solidity
function setPoolOperationPause(uint256 poolId, enum PoolOperationPausable.Operation operation, bool paused) external nonpayable
```

Set the `paused` status of `operation` for `poolId` pool.

#### Parameters

| Name      | Type                                 | Description                |
| --------- | ------------------------------------ | -------------------------- |
| poolId    | uint256                              | The index of staking pool. |
| operation | enum PoolOperationPausable.Operation | The user operation.        |
| paused    | bool                                 | The pause status.          |

### setRewardsDeductionRate

```solidity
function setRewardsDeductionRate(uint256 poolId, uint256 rate) external nonpayable
```

Set deduction `rate` of claim rewards for `poolId` pool.

#### Parameters

| Name   | Type    | Description                      |
| ------ | ------- | -------------------------------- |
| poolId | uint256 | The index of staking pool.       |
| rate   | uint256 | The deduction rate. 1e18 is 100% |

### transferOwnership

```solidity
function transferOwnership(address newOwner) external nonpayable
```

_Transfers ownership of the contract to a new account (`newOwner`). Can only be called by the current owner._

#### Parameters

| Name     | Type    | Description |
| -------- | ------- | ----------- |
| newOwner | address | undefined   |

### unpause

```solidity
function unpause() external nonpayable
```

Unpuase the contract by Pausable.

_Define the `onlyOwner` access._

### updateRewardRule

```solidity
function updateRewardRule(uint256 poolId, contract IERC20 rewardType, uint256 rewardRate, uint256 endTime) external nonpayable
```

Update the reward rule of `rewardType` for `poolId` pool.

_Override the inherited function to define `onlyOwner` and `whenNotPaused` access._

#### Parameters

| Name       | Type            | Description                   |
| ---------- | --------------- | ----------------------------- |
| poolId     | uint256         | The index of staking pool.    |
| rewardType | contract IERC20 | The reward token.             |
| rewardRate | uint256         | The reward amount per second. |
| endTime    | uint256         | The end time of fule.         |
