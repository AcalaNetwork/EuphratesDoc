# Governance

The owner of `ProxyAdmin` contract controls `TransparentUpgradeableProxy` upgrade. The owner of `TransparentUpgradeableProxy` has the authority to configure the parameters of Euphrates and pause/unpuase the whole `TransparentUpgradeableProxy` contract. In erally stage, both owners are Acala Foundation multisig. Generally, Acala foundation will not manage Euphrates directly through multisig, unless the contract needs to be paused in an emergency. Euphrates smart contract integrates with Acala/Substrate on-chain governance, where multisig rights will be migrated to be under the jurisdiction of on-chain governance.



## Governance Methods

### addPool

```solidity
function addPool(contract IERC20 shareType) external nonpayable
```

Initialize a staking pool for `shareType`.

#### Parameters

| Name | Type | Description |
|---|---|---|
| shareType | contract IERC20 | The share token. |

### claimRewards

```solidity
function claimRewards(uint256 poolId) external nonpayable returns (bool)
```

Claim all rewards from staking pool.

#### Parameters

| Name | Type | Description |
|---|---|---|
| poolId | uint256 | The index of staking pool. |


### convertLSTPool

```solidity
function convertLSTPool(uint256 poolId, enum UpgradeableStakingLST.ConvertType convertType) external nonpayable
```

convert the share token of ‘poolId’ pool to LST token by `convertType`.

#### Parameters

| Name | Type | Description |
|---|---|---|
| poolId | uint256 | The index of staking pool. |
| convertType | enum UpgradeableStakingLST.ConvertType | The convert type. |

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

| Name | Type | Description |
|---|---|---|
| poolId | uint256 | The index of staking pool. |
| operation | enum PoolOperationPausable.Operation | The user operation. |
| paused | bool | The pause status. |

### setRewardsDeductionRate

```solidity
function setRewardsDeductionRate(uint256 poolId, uint256 rate) external nonpayable
```

Set deduction `rate` of claim rewards for `poolId` pool.

#### Parameters

| Name | Type | Description |
|---|---|---|
| poolId | uint256 | The index of staking pool. |
| rate | uint256 | The deduction rate. 1e18 is 100% |

### transferOwnership

```solidity
function transferOwnership(address newOwner) external nonpayable
```



*Transfers ownership of the contract to a new account (`newOwner`). Can only be called by the current owner.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| newOwner | address | undefined |

### unpause

```solidity
function unpause() external nonpayable
```

Unpuase the contract by Pausable.

*Define the `onlyOwner` access.*

### updateRewardRule

```solidity
function updateRewardRule(uint256 poolId, contract IERC20 rewardType, uint256 rewardRate, uint256 endTime) external nonpayable
```

Update the reward rule of `rewardType` for `poolId` pool.

*Override the inherited function to define `onlyOwner` and `whenNotPaused` access.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| poolId | uint256 | The index of staking pool. |
| rewardType | contract IERC20 | The reward token. |
| rewardRate | uint256 | The reward amount per second. |
| endTime | uint256 | The end time of fule. |
