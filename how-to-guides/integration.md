# Integration

### API

#### Convert rate

```
<https://farm.acala.network/api/convert_rate>
```

#### tDOT apr

```
<https://api.taigaprotocol.io/rewards/apr?network=acala&pool=0>
```

#### Pool apr graph

```
<https://farm.acala.network/api/apr/{poolId}>
```

**Parameters**

The only required query parameter is `poolId`

#### ACA and DOT price

```
<https://api.coingecko.com/api/v3/simple/price?ids=polkadot,acala&vs_currencies=usd&precision=18>
```

#### Search-related API

**Query the user’s LCDOT balance in Acala**

```
<https://acala.api.subscan.io/api/v2/scan/search>
```

**Parameters**

| Parameter       | Type   | Description                           |
| --------------- | ------ | ------------------------------------- |
| page            | number | page index                            |
| value range ≥ 0 |        |                                       |
| row             | number | number of row to be returned per page |
| value range ≥ 0 |        |                                       |
| key             | string | filter by contributor address         |

**Query the user’s contribution in polkadot.js**

```
<https://polkadot.api.subscan.io/api/scan/account/contributions>
```

**Parameters**

| Parameter       | Type   | Description                           |
| --------------- | ------ | ------------------------------------- |
| page            | number | page index                            |
| value range ≥ 0 |        |                                       |
| row             | number | number of row to be returned per page |
| value range ≥ 0 |        |                                       |
| who             | string | filter by contributor address         |

**Query the user’s cDOT balance in parallel**

* cDOT-6/13 200060013
* cDOT-7-14 200070014
* cDOT-8/15 200080015

```jsx
<https://polkadot.api.subscan.io/api/scan/multiChain/account>
```

**Parameters**

| Parameter | Type   | Description                   |
| --------- | ------ | ----------------------------- |
| address   | string | filter by contributor address |

### Subquery

#### LDOT APY

```
<https://api.polkawallet.io/acala-liquid-staking-subql>

Examples:
{
  query {
    dailySummaries(first: 30, orderBy: TIMESTAMP_DESC) {
      nodes {
        exchangeRate
        timestamp
      }
    }
  }
}
```

#### LCDOT, LDOT, TDOT, WTDOT price

```
<https://api.polkawallet.io/acala-dex-subql>

Examples:
query {
  swaps(orderBy: TIMESTAMP_DESC, first: 1, filter: { poolId: { equalTo: "lp://DOT/lc%3A%2F%2F13" } }) {
    nodes {
      poolId
      token0Id
      token1Id
      token0InAmount
      token1OutAmount
      timestamp
      id
    }
  }

  stableAssetSwaps(orderBy: TIMESTAMP_DESC, first: 1, filter: { poolId: { equalTo: 0 } }) {
    nodes {
      price
      timestamp
      id
      poolId
    }
  }
}
```

price calculation:

```jsx
// result equals the result returned by subquery
base = result.swaps.nodes[0].token0Id === 'DOT'
	? result.swaps.nodes[0].token0InAmount
	: result.swaps.nodes[0].token1OutAmount;
target = result.swaps.nodes[0].token0Id === 'DOT'
	? result.swaps.nodes[0].token1OutAmount
	: result.swaps.nodes[0].token0InAmount

// dotPrice = [ACA and DOT price](<https://www.notion.so/Integration-2e437289d2a34c24bd729b7d11c16a1f?pvs=21>)
LDOT_Price = dotPrice / (target / base)
LCDOT_Price = dotPrice / result.stableAssetSwaps.nodes[0].price
TDOT_Price = dotPrice
WTDOT_Price = dotPrice

```
