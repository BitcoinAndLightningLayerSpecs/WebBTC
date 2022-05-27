# Enable Wallet

The `enable` method is called to allow access to further API methods from the wallet.

## Syntax

```
enable()
```

## Parameters

None

## Returns

  - Object
    - enabled : Boolean <span class="badge">Required</span>
    - addresses : AddressObjArray <span class="badge">Optional</span>
        - address: String
        - derivationPath: String
        - publicKey: String

> **_NOTE:_**  
The AddressObjArray here can be returned for Onchain wallets but can also be used ny WebLN wallets which also expose the onchain wallet functions. This typically is used to show that a wallet is connected to the page. 

![ENABLED ON WEBSITE](/assets/enable.png)

## Example

```
// Enable wallet
window.webbtc.enable()

{
  address: {
    address: "bc1q9zw3q496dcx2qu5pvhvg0zwfsxgj79nhh5rqct"
    derivationPath: "84'/0'/0'/0/0"
    publicKey: "031ecb71f390fcffc8727bedc5fb563e7bf90cd9725b1519e1ef74a16ca7a30fe3"
  },
  success: true
}
```

```
// Check if the wallet is enabled 
window.webbtc.enabled 

true
```

```
// Check if wallet is enabled, invoke enable when false
if (!window.webbtc.enabled) window.webbtc.enable()
```
## Notes

Application specific on wether or not to trust once or always. On invoking the `enable` call the application developer provides an interface which may or may not prompt the user to accept the request.