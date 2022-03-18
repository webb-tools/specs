# Token Wrapping Protocol

## Overview
The token wrapping protocol is a protocol to wrap native and non-native assets into a new wrapped token. These wrapped tokens are inserted into the Webb Protocol **Anchors** and are used to transfer assets between the **Anchors**.

The token wrapping protocol is intended to be built on top of:
- ERC20 Interfaces (EVM)
- CW20 Interfaces (CosmWasm)
- PSP20 Interfaces (Substrate Ink!)
- ORML interfaces (Substrate ORML)

## High-level architectures
The token wrapping protocol defines an API that allows users to wrap assets and unwrap assets. Currently, the token wrapping protocol specifies a **1-to-1** wrapping system. That is, wrapping 1 valid token will mint 1 wrapped token.

#### `wrap(token, amount)`
- `token`: The token to wrap (an address of an ERC20 or CW20 contract for example)
- `amount`: The amount of tokens to wrap.

#### `unwrap(token, amount)`
- `token`: The token to unwrap into (an address of an ERC20 or CW20 contract for example)
- `amount`: The amount of tokens to unwrap.