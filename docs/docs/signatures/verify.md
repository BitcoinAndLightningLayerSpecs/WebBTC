# Verify Message Signature

The `verifyMessage` method is used to verify the signature of a arbitrary message.

## Syntax

```
verifyMessage(signature, address?)
```

## Parameters

  - Object
    - signature: String (Hex) - The message to sign
    - address: String - The used to sign the message

> **_NOTE:_**  
  The second parameter here is typically required for onchain wallets but can be omitted if the wallet contains internal support for automatic key selection. In the event of LND or C-Lightning, the wallet may use a root key whereas onchain wallets require to provide the address derived from the key required for signing the message.

## Returns

- Boolean - Is valid signature

## Example

```
> await window.webbtc.verifyMessage('2047ab7b010687146ef9d69648cbdc4610b7ebaf6f21d7255f2113fe87b24d4b4264eef980d21f29d3ba81b369e41bf532b1292021af16c6773187c34d090b7efb', 'tb1qqwn2dp8mundc6mf3xt4c8puqakk0vrcgzdayq2')

true
```

##References

[VerifyMessage LND](https://api.lightning.community/#verifymessage)

[lightning-checkmessage C-lightning](https://lightning.readthedocs.io/lightning-checkmessage.7.html)

Bitcoin Core

- [Signatures of Messages using Private Keys- BIP137](https://github.com/bitcoin/bips/blob/master/bip-0137.mediawiki)
- [Generic Signed Message Format BIP322](https://github.com/bitcoin/bips/blob/master/bip-0322.mediawiki)