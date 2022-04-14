# Price Oracle

Throughout the Aave Protocol, we require reliable, up to date, and secure price feeds. Our proxy price provider contract provides this capability and works by:

{% tabs %}
{% tab title="Aave market" %}
1. First checking for a price from a Chainlink aggregator.
2. If the price is below or equal to zero, we call our [fallback price oracle.](./#getfallbackoracle)​
   1. The fallback price oracle is currently maintained by the Aave team.
3. In the future, Aave governance mechanisms will manage the selection of sources and the fallback price oracle.
{% endtab %}
{% endtabs %}

The source code can be found on the [verified Etherscan contract](../../deployed-contracts/deployed-contracts.md).

If you need development support, join the #developers channel on our [Aave community Discord server](https://discord.gg/fVaDMqT).

{% hint style="warning" %}
Always get the latest price oracle address by calling [`getPriceOracle()`](../addresses-provider/#getpriceoracle) on the [`LendingPoolAddressProvider`](../addresses-provider/) contract.
{% endhint %}

## View Methods <a href="#view-methods" id="view-methods"></a>

### getAssetPrice**()** <a href="#getassetprice" id="getassetprice"></a>

**`function getAssetPrice(address _asset) public view returns(uint256)`**

Returns the price of the supported `_asset` in ETH wei units.

| Parameter Name | Type    | Description                                                                                         |
| -------------- | ------- | --------------------------------------------------------------------------------------------------- |
| `_asset`       | address | address of the [underlying asset](../../deployed-contracts/deployed-contracts.md#supported-assets)​ |

### getAssetsPrices**()** <a href="#getassetsprices" id="getassetsprices"></a>

**`function getAssetsPrices(address[] calldata _assets) external view returns(uint256[] memory)`**

Returns any array of prices in ETH wei units.

| Parameter Name | Type        | Description                                                                                                        |
| -------------- | ----------- | ------------------------------------------------------------------------------------------------------------------ |
| `_assets`      | address\[ ] | an array of addresses of the [underlying assets](../../deployed-contracts/deployed-contracts.md#supported-assets)​ |

### getSourceOfAsset()

**`function getSourceOfAsset(address _asset) external view returns(uint256)`**

Returns the address of the price source for `_asset`.

| Parameter Name | Type    | Description                                                                                         |
| -------------- | ------- | --------------------------------------------------------------------------------------------------- |
| `_asset`       | address | address of the [underlying asset](../../deployed-contracts/deployed-contracts.md#supported-assets)​ |

### getFallbackOracle**()** <a href="#getfallbackoracle" id="getfallbackoracle"></a>

**`function getFallbackOracle() external view returns(uint256)`**

Returns the address of the fallback oracle.



