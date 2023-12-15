# Integration

## API

### Total DOT Locked

Total LDOT and tDOT Locked in LSTs on Acala

{% code overflow="wrap" %}
```javascript
Method: HTTP-GET
URL: https://farm.acala.network/api/total_locked
```
{% endcode %}

### TVL

TVL of the LST pool

```jsx
Method: HTTP-GET
URL: https://farm.acala.network/api/tvl
```

### tDOT APR

```jsx
Method: HTTP-GET
URL: https://api.taigaprotocol.io/rewards/apr?network=acala&pool=0
```

### StellaSwap LP TVL

```javascript
Method: GraphQL
URL: https://api.thegraph.com/subgraphs/name/stellaswap/pulsar

Query:
{
  pool(id: "0x6bb200b706ffa1665127877a11588221c49d9eed") {
    totalValueLockedUSD
  }
}
```

### StellaSwap Trading fees APR

```javascript
Method: HTTP
URL: https://apr-api.stellaswap.com/api/v1/poolsAPR/

Find value of 0x6bb200b706ffa1665127877a11588221c49d9eed
```

### StellaSwap Farm APR

```javascript
Method: HTTP
URL: https://apr-api.stellaswap.com/api/v1/poolsAPR/

Find value of 0x6bb200b706ffa1665127877a11588221c49d9eed
rewardTokenApr is ACA's APR
bonusToken is STELLA's APR
lastApr = rewardTokenApr + bonusToken
```

### Token Price

```jsx
Method: HTTP-GET
URL: https://farm.acala.network/api/token_prices
```

### Pools Details

LST pool details

```jsx
Method: HTTP-GET
URL: https://farm.acala.network/api/pools/{poolId}
```

**Parameters**

The only required query parameter is `poolId`

### Dapp Version

Front-end version update prompt

```jsx
Method: HTTP-GET
URL: https://farm.acala.network/api/version
```

### Pool TVL History

Historical TVL data of LST pool

```jsx
Method: HTTP-GET
URL: https://farm.acala.network/api/tvl/{poolId}
```

**Parameters**

The only required query parameter is `poolId`

### LCDOT in Acala

The user’s LCDOT balance in Acala

```jsx
Method: HTTP-POST
URL: https://acala.api.subscan.io/api/v2/scan/search

Find asset_registry/bfa7a23dc17bb490d4032c78cbc87babb4eb6f74 in response
```

**Parameters**

| Parameter       | Type   | Description                           |
| --------------- | ------ | ------------------------------------- |
| page            | number | page index                            |
| value range ≥ 0 |        |                                       |
| row             | number | number of row to be returned per page |
| value range ≥ 0 |        |                                       |
| key             | string | filter by contributor address         |

### LCDOT in Polkadot{.js}

The user’s contribution in Polkadot{.js}

```jsx
Method: HTTP-POST
URL: https://polkadot.api.subscan.io/api/scan/account/contributions

Find para_id in response
para_id: {
	'2000': 'Acala',
	'2002': 'Clover',
	'2004': 'Moonbeam',
	'2006': 'Astar',
	'2012': 'Parallel',
	'2030': 'Bifrost',
	'2031': 'Centrifuge',
	'2035': 'Phala Network',
	'2021': 'Efinity',
	'2019': 'Composable Finance',
	'2032': 'Interlay',
	'2026': 'Nodle',
	'2034': 'HydraDX',
}
```

**Parameters**

| Parameter       | Type   | Description                           |
| --------------- | ------ | ------------------------------------- |
| page            | number | page index                            |
| value range ≥ 0 |        |                                       |
| row             | number | number of row to be returned per page |
| value range ≥ 0 |        |                                       |
| who             | string | filter by contributor address         |

### **LCDOT in Parallel**

The user’s cDOT balance in Parallel

```jsx
Method: HTTP-POST
URL: https://polkadot.api.subscan.io/api/scan/multiChain/account

Find LCDOT in response
- cDOT-6/13 200060013
- cDOT-7-14 200070014
- cDOT-8/15 200080015
```

**Parameters**

| Parameter | Type   | Description                   |
| --------- | ------ | ----------------------------- |
| address   | string | filter by contributor address |

## Subquery

### LDOT APR

```jsx
Method: HTTP-POST
URL: https://api.polkawallet.io/acala-liquid-staking-subql

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

Calculation: 
const exchangeRates = result.query.dailySummaries.nodes;

const first = exchangeRates[0];
const last = exchangeRates[exchangeRates.length - 1];
const len = exchangeRates.length;

const apr = (first.exchangeRate / last.exchangeRate - 1) * (365 / len);
```
