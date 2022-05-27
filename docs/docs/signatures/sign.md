# Sign Message 

The `signMessage` method is used to sign arbitrary data and produce a signature which can be used to verify ownership of a key.

## Syntax

```
signMessage(message, address?)
```

## Parameters
  - Object
    - message: String - The message to sign <span class="badge">Required</span>
    - address: Object <span class="badge">Option</span>

> **_NOTE:_**  
  The second parameter here is typically required for onchain wallets but can be omitted if the wallet contains internal support for automatic key selection. In the event of LND or C-Lightning, the wallet may use a root key whereas onchain wallets require to provide the address derived from the key required for signing the message.

## Returns

- Signature: String <span class="badge">Required</span>

## Example

```
> await window.wallet.signMessage('Better with code than with words', 'tb1qqwn2dp8mundc6mf3xt4c8puqakk0vrcgzdayq2')

"2047ab7b010687146ef9d69648cbdc4610b7ebaf6f21d7255f2113fe87b24d4b4264eef980d21f29d3ba81b369e41bf532b1292021af16c6773187c34d090b7efb"
```

## References

### WebLN examples
[https://api.lightning.community/#chainrpc-spendrequest](https://api.lightning.community/#chainrpc-spendrequest)

### BIPS

[https://github.com/bitcoin/bips/blob/master/bip-0137.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0137.mediawiki)
[https://github.com/bitcoin/bips/blob/master/bip-0322.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0322.mediawiki)

### C-lightning
[https://lightning.readthedocs.io/lightning-signmessage.7.html](https://lightning.readthedocs.io/lightning-signmessage.7.html)