# Addresses Provider

## LendingPoolAddressesProvider

Addresses register of the protocol for a particular market. This contract is immutable and the address will never change. Also see [Deployed Contracts](../../deployed-contracts/deployed-contracts.md) section.

{% hint style="info" %}
Whenever the `LendingPool` contract is needed, we recommended you fetch the correct address from the `LendingPoolAddressesProvider` smart contract.
{% endhint %}

The source code can be [found on Github here](https://github.com/aave/protocol-v2/blob/ice/mainnet-deployment-03-12-2020/contracts/protocol/configuration/LendingPoolAddressesProvider.sol).

## Methods

### getMarketId**()**

**`function getMarketId()`**

#### Return values

| Type   | Description                           |
| ------ | ------------------------------------- |
| string | A string representation of the market |

### getLendingPool**()**

**`function getLendingPool()`**

#### Return values

| Type    | Description                                                  |
| ------- | ------------------------------------------------------------ |
| address | The address of the associated [LendingPool](../lendingpool/) |

### getLendingPoolConfigurator**()**

**`function getLendingPoolConfigurator()`**

The `LendingPoolConfigurator` is used for configuration methods for each market, e.g.initialising a reserve or updating aTokens.

#### Return values

| Type    | Description                                            |
| ------- | ------------------------------------------------------ |
| address | The address of the associated `LendingPoolConfiguator` |

### getLendingPoolCollateralManager**()**

**`function getLendingPoolCollateralManager()`**

The `LendingPoolCollateralManager` is used for management of collateral in the protocol, the main one being for liquidations. The contract should never be called directly, only via the `LendingPool`.

#### Return values

| Type    | Description                                                  |
| ------- | ------------------------------------------------------------ |
| address | The address of the associated `LendingPoolCollateralManager` |

### getPoolAdmin**()**

**`function getPoolAdmin()`**

#### Return values

| Type    | Description                              |
| ------- | ---------------------------------------- |
| address | The address of the market / pool's admin |

### getPoolEmergencyAdmin**()**

**`function getPoolEmergencyAdmin()`**

#### Return values

| Type    | Description                                        |
| ------- | -------------------------------------------------- |
| address | The address of the market / pool's emergency admin |

### getPriceOracle**()**

**`function getPriceOracle()`**

#### Return values

| Type    | Description                     |
| ------- | ------------------------------- |
| address | The address of the price oracle |

### getLendingRateOracle**()**

**`function getLendingRateOracle()`**

#### Return values

| Type    | Description                            |
| ------- | -------------------------------------- |
| address | The address of the `LendingRateOracle` |

### getAddress**()**

**`function getAddress(bytes32 id)`**

For example, the [Protocol Data Provider](../protocol-data-provider/) uses the id: `0x1`

#### Return values

| Type    | Description                                       |
| ------- | ------------------------------------------------- |
| address | The address associated with the `bytes32` id used |
