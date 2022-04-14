# WETH Gateway

If you need to use native ETH (MATIC / AVAX in case of side chain market) in the protocol, it must first be wrapped into WETH (or WMATIC / WAVAX). The WETH Gateway contract is a helper contract to easily wrap and unwrap ETH (or MATIC / AVAX) as necessary when interacting with the protocol, since only ERC20 is used within protocol interactions.

The source code can be [found here](https://github.com/aave/protocol-v2/blob/master/contracts/misc/WETHGateway.sol), with the latest deployed address listed in the [Deployed Contracts](../deployed-contracts/deployed-contracts.md).

## Methods

### depositETH**()**

**`function depositETH(address lendingPool, address onBehalfOf, uint16 referralCode)`**

Deposits the `msg.value` amount of ETH into the protocol, minting the same amount of corresponding aWETH, and transferring them to the `onBehalfOf` address.

For `referralCode` input explanations, please refer to the[ referral program section](broken-reference) of the documentation. During testing, you can use the referral code: `0`.

{% hint style="warning" %}
Ensure that the `depositETH()` transaction also includes the amount of ETH you are depositing in the `msg.value`.
{% endhint %}

| Parameter Name | Type    | Description                                                                                                                |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------------------------- |
| `lendingPool`  | address | address of the targeted underlying lending pool                                                                            |
| `onBehalfOf`   | address | <p>address whom will receive the aWETH. <br>Use <code>msg.sender</code> when the aTokens should be sent to the caller.</p> |
| `referralCode` | uint16  | referral code for our [referral program](broken-reference). Use 0 for no referral.                                         |

### withdrawETH**()**

**`function withdrawETH(address lendingPool, uint256 amount, address to)`**

Withdraws `amount` of the WETH, unwraps it to ETH, and transfers the ETH to the `to` address.

{% hint style="warning" %}
Ensure you set the relevant ERC20 allowance of aWETH, before calling this function, so the `WETHGateway` contract can burn the associated aWETH.
{% endhint %}

| Parameter Name | Type    | Description                                                                                                          |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------------------- |
| `lendingPool`  | address | address of the targeted underlying lending pool                                                                      |
| `amount`       | uint256 | <p>amount deposited, expressed in wei units. <br>Use <code>type(uint).max</code> to withdraw the entire balance.</p> |
| `to`           | address | address that will receive the unwrapped ETH                                                                          |

### repayETH**()**

**`function repayETH(address lendingPool, uint256 amount, uint256 rateMode, address onBehalfOf)`**

Repays `onBehalfOf`'s debt `amount` of ETH which has a `rateMode`.

{% hint style="warning" %}
Ensure that the `repayETH()` transaction also includes the amount of ETH you are repaying in the `msg.value`.
{% endhint %}

| Parameter Name | Type    | Description                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `lendingPool`  | address | address of the targeted underlying lending pool                                                                                                                                                                                                                                                                                                                |
| `amount`       | uint256 | <p>amount to be borrowed, expressed in wei units.</p><p>Use <code>uint(-1)</code> to repay the entire debt,  <strong>ONLY</strong> when the repayment is not executed on behalf of a 3rd party. </p><p>In case of repayments on behalf of another user, it's recommended to send an <code>_amount</code> slightly higher than the current borrowed amount.</p> |
| `rateMode`     | uint256 | <p>the type of borrow debt.</p><p>Stable: 1, Variable: 2</p>                                                                                                                                                                                                                                                                                                   |
| `onBehalfOf`   | address | <p>address of user who will incur the debt.</p><p>Use <code>msg.sender</code> when not calling on behalf of a different user.</p>                                                                                                                                                                                                                              |

### borrowETH**()**

**`function borrowETH(address lendingPool, uint256 amount, uint256 interestRateMode, uint16 referralCode)`**

Borrows `amount` of WETH with `interestRateMode`, sending the `amount` of unwrapped WETH to `msg.sender`.

| Parameter Name     | Type    | Description                                                                             |
| ------------------ | ------- | --------------------------------------------------------------------------------------- |
| `lendingPool`      | address | address of the targeted underlying lending pool                                         |
| `amount`           | uint256 | amount to be borrowed, expressed in wei units                                           |
| `interestRateMode` | uint256 | <p>the type of borrow debt.</p><p>Stable: 1, Variable: 2</p>                            |
| `referralCode`     | uint16  | referral code for our [referral program](broken-reference). Use 0 for no referral code. |

## View Methods

### getWETHAddress**()**

**`function getWETHAddress()`**

Returns the WETH address used by the WETHGateway.

