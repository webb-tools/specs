# Token Wrapping Protocol

## Overview
The token wrapping protocol is a protocol to wrap native and non-native assets into a new wrapped token. These wrapped tokens are inserted into the Webb Protocol **Anchors** and are used to transfer assets between the **Anchors**.

The token wrapping protocol is intended to be built on top of:
- ERC20 Interfaces (EVM)
- CW20 Interfaces (CosmWasm)
- PSP20 Interfaces (Substrate Ink!)
- ORML interfaces (Substrate ORML)

## Base Architecture
The token wrapping protocol defines an API that allows users to wrap assets and unwrap assets.

### Validation functions
A token contract implementing the token wrapping protocol can specify a variety of parameters necessary for validation of inputs to state-changing functions. We start be outlining the necessary parameters and discuss extraneous parameters after.

#### `isValidAddress(token) -> bool`
Checks if a `token` is valid in order to proceed with a state-changing action such as wrapping or unwrapping.
- `token`: The token to check
  - An address of an ERC20 or CW20 contract if non-zero / non-null
  - A native token zero / null

#### `isNativeValid() -> bool`
Checks if a native asset is valid for wrapping.

#### `isValidAmount(amount) -> bool`
Checks if the amount to be wrapped or unwrapped is valid.

### State-changing Functions
The state changing API defines the set of functions that mutate the state of the contract implementing the token wrapping protocol.

#### `wrap(token, amount)`
Wraps an `amount` of `token` into the `amount` of the underlying wrapped token.
- `token`: The token to wrap
  - An address of an ERC20 or CW20 contract if non-zero / non-null
  - A native token zero / null
- `amount`: The amount of tokens to wrap.

##### Validity conditions
1. If the token is `null` or `0`, the function should wrap the ***native*** asset if and only if native wrapping is supported.
2. If the token is not `null`, the function should wrap the ***token*** if and only if the the token is supported for wrapping.

#### `unwrap(token, amount)`
Unwraps an `amount` of the underlying wrapped token into the amount of `token`.
- `token`: The token to unwrap into
  - An address of an ERC20 or CW20 contract if non-zero / non-null
  - A native token zero / null
- `amount`: The amount of tokens to unwrap.

##### Validity conditions
1. If the token is `null` or `0`, the function should unwrap into the ***native*** asset if and only if native unwrapping is supported.
2. If the token is not `null`, the function should unwrap the ***token*** if and only if the the token is supported for unwrapping.

## Extensions
### Governable Token Wrapping
The token wrapping protocol can be extended to support governance. This is a main feature to be implemented with any contract implementing the token wrapping protocol.
#### Governable Parameters
- The valid tokens that can be wrapped
- The valid amounts that can be wrapped
- The multipliers of tokens that can be wrappedg

### Wrapping Parameters
Currently, existing token wrapper protocol implementations employ a 1-to-1 wrapping system. We can consider generalizing this.
#### `wrappingMultiplier(token) -> Percentage`
Takes a `token` and outputs a percentage to be used to determine the amount of the underlying wrapped token to wrap.

##### Implementation details
This would be maintained likely through the use of a mapping between tokens and percentages.
