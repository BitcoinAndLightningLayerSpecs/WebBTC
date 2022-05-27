# Get addresses from wallet

The `getAddresses` method is called to obtain an address from the onchain wallet of the wallet. 

> **_NOTE:_**  
WebLN implementations might choose to implement this method when exposing access to the onchain wallet. 

## Syntax

```
getAddresses(index?, num?, change?)
```

## Parameters

- index: Number (default 0) - Which index to start from <span class="badge">Optional</span>
- num: Number (default 1) - Number of addresses to retrieve <span class="badge">Optional</span>
- change: Boolean (default false) - true for change addresses, false for external <span class="badge">Optional</span>

## Returns

- AddressObjectArray - An array of bitcoin address objects <span class="badge">Required</span>
    - address: String - Bitcoin address <span class="badge">Required</span>
    - derivationPath: String - Derivation path of the address e.g. "84'/1'/0'/0/0" <span class="badge">Optional</span>
    - publicKey: String(Hex) - The public key for the derivation path <span class="badge">Optional</span>
    - index: Number - Index of the address <span class="badge">Optional</span>

## Example

```
await window.webbtc.getAddresses(0, 10, false)
[{
    address: "tb1qqwn2dp8mundc6mf3xt4c8puqakk0vrcgzdayq2",
    derivationPath: "84'/1'/0'/0/0",
    publicKey: {
        …},
    index: 0
} {
    address: "tb1qca6k2ke5jdrwmdqcku4eex4k9hzzzhzshhsgpn",
    derivationPath: "84'/1'/0'/0/1",
    publicKey: {
        …},
    index: 1
} {
    address: "tb1q6e36gyc8vhv97k9m2uldndsl8xg80yd49mhqpx",
    derivationPath: "84'/1'/0'/0/2",
    publicKey: {
        …},
    index: 2
} {
    address: "tb1qvphc32p0qxl2fm89r04epmtxvdt7l7dl5a955c",
    derivationPath: "84'/1'/0'/0/3",
    publicKey: {
        …},
    index: 3
} {
    address: "tb1qxm90ahvjnut9d7mw8d0r22czldnu3kqyef55nn",
    derivationPath: "84'/1'/0'/0/4",
    publicKey: {
        …},
    index: 4
} {
    address: "tb1q8wjjk4gu3am2tjg833qulqt69ny8e24vt8ccj6",
    derivationPath: "84'/1'/0'/0/5",
    publicKey: {
        …},
    index: 5
} {
    address: "tb1q7jkkn80maps9z068u22jrpv65t9epjlrl4zpzj",
    derivationPath: "84'/1'/0'/0/6",
    publicKey: {
        …},
    index: 6
} {
    address: "tb1qrzpw5rrm9w8qf3v3y43av3npeqhgp9lng5xtyk",
    derivationPath: "84'/1'/0'/0/7",
    publicKey: {
        …},
    index: 7
} {
    address: "tb1q9vu3j2m6u48sv53g7e24lfx2c9mavv0ee6wr02",
    derivationPath: "84'/1'/0'/0/8",
    publicKey: {
        …},
    index: 8
} {
    address: "tb1q0m2f0vjc4njy5d0vzmlwre8jdtar9x9w7nz9jg",
    derivationPath: "84'/1'/0'/0/9",
    publicKey: {
        …},
    index: 9
}]
```

## Notes

Implemented for on-chain, might however not be supported by off-chain wallets