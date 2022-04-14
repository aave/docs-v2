# Protocol Data Provider

The purpose of this contract is to help integrators and developers more easily leverage the Aave Protocol data and features.

If you need development support,  join the #developers channel on the [Aave community Discord server](https://discord.gg/CJm5Jt3).

The source code can be found [on Github here](https://github.com/aave/protocol-v2/blob/ice/mainnet-deployment-03-12-2020/contracts/misc/AaveProtocolDataProvider.sol).

{% hint style="info" %}
Each market has a separate Protocol Data Provider. To get the address for a particular market, call [`getAddress()`](../addresses-provider/#getaddress) using the value `0x1.`
{% endhint %}

## Methods

### getAllReservesTokens**()**

**`function getAllReservesTokens()`**

Returns an array of all reserve tokens for the current market, in the form of a TokenData struct consisting of the token symbol and token address.

#### Return values

| Type          | Description                                                                         |
| ------------- | ----------------------------------------------------------------------------------- |
| TokenData\[ ] | A struct consisting of a `symbol` of type string and `tokenAddress` of type address |

### getAllATokens**()**

**`function getAllATokens()`**

Returns an array of all aTokens for the current market, in the form of a TokenData struct consisting of the token symbol and token address.

#### Return values

| Type          | Description                                                                         |
| ------------- | ----------------------------------------------------------------------------------- |
| TokenData\[ ] | A struct consisting of a `symbol` of type string and `tokenAddress` of type address |

### getReserveConfigurationData**()**

**`function getReserveConfigurationData(address asset)`**

Returns the configuration data for `asset`.

#### Return values

| Type    | Description                                                            |
| ------- | ---------------------------------------------------------------------- |
| uint256 | decimals: the decimals used by the reserve                             |
| uint256 | ltv: the Loan To Value                                                 |
| uint256 | liquidationThreshold: the liquidation threshold of the reserve         |
| uint256 | liquidationBonus: the bonus awarded to liquidators                     |
| uint256 | reserveFactor: the reserve factor                                      |
| bool    | usageAsCollateralEnabled: whether the reserve is enabled as collateral |
| bool    | borrowingEnabled: whether borrowing is enabled on the reserve          |
| bool    | stableBorrowRateEnabled: whether stable borrowing is enabled           |
| bool    | isActive: whether the reserve is active                                |
| bool    | isFrozen: whether the reserve is frozen / disabled                     |

### getReserveData**()**

**`function getReserveData(address asset)`**

Returns the associated data for `asset`.

#### Return values

| Type    | Description                                                               |
| ------- | ------------------------------------------------------------------------- |
| uint256 | availableLiquidity: the amount of liquidity available                     |
| uint256 | totalStableDebt: the total amount of debt borrowed at the stable rate     |
| uint256 | totalVariableDebt: the total amount of debt borrowed at the variable rate |
| uint256 | liquidityRate: the interest rate for deposits / adding liquidity          |
| uint256 | variableBorrowRate: the interest rate for borrowing at a variable rate    |
| uint256 | stableBorrowRate: the interest rate for borrowing at a stable rate        |
| uint256 | averageStableBorrowRate: the current average stable borrow rate           |
| uint256 | liquidityIndex: the index used in liquidity calculations                  |
| uint256 | variableBorrowIndex: the index used in variable debt calculations         |
| uint40  | lastUpdateTimestamp: the timestamp of the reserve's last update           |

### getUserReserveData**()**

**`function getUserReserveData(address asset, address user)`**

Returns the `user`'s reserve data for `asset`.

#### Return values

| Type    | Description                                                                             |
| ------- | --------------------------------------------------------------------------------------- |
| uint256 | currentATokenBalance: current aToken balance of `user`                                  |
| uint256 | currentStableDebt: current stable debt  the `user`                                      |
| uint256 | currentVariableDebt: current variable debt of the `user`                                |
| uint256 | principalStableDebt: the principal stable debt of the `user`                            |
| uint256 | scaledVariableDebt: the scaled variable debt of the `user`                              |
| uint256 | stableBorrowRate: the stable borrow rate of the `user`                                  |
| uint256 | liquidityRate: the interest rate being earned by the user for deposits                  |
| uint40  | stableRateLastUpdated: the timestamp of the last stable rate update                     |
| bool    | usageAsCollateralEnabled: whether the `reserve` is enabled as collateral for the `user` |

### getReserveTokensAddresses**()**

**`function getReserveTokensAddresses(address asset)`**

Returns the associated addresses for an `asset`

#### Return values

| Type    | Description                                                               |
| ------- | ------------------------------------------------------------------------- |
| address | aTokenAddress: the address of the tokenised deposit                       |
| address | stableDebtTokenAddress: the address of the tokenised stable rate debt     |
| address | variableDebtTokenAddress: the address of the tokenised variable rate debt |

