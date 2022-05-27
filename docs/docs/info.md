# Get wallet information

The `getInfo` method is called to obtain supported features and capabilities of the wallet. 

## Syntax

```
getInfo()
```

## Parameters

None

## Returns

- Object
    - version : Number | String <span class="badge">Required</span>
    - methods : Array <span class="badge">Optional</span>
    - supports : Array <span class="badge">Optional</span>

## Example

```
window.webbtc.getInfo()

{ 
  "version" : 1,
  "supports" : [
    "bip39",
    "bip32"
  ],
  "methods": [ // schema for available methods
    "enable",
    "getInfo",
    "getAddress",
    "signMessage",
    "verifyMessage",
    "makeInvoice",
    "sendPayment"
  ]
}
```

## Additional notes

The above method might be extended to include helper methods which include. 

- `window.webbtc.getMethods()`
- `window.webbtc.getVersion()`
- `window.webbtc.getServices()`

> **_NOTE:_**
  Method for obtaining existing supported permissions that the user could approve when enabling the wallet. Application specific implementation details can vary based on the security preference. 

## Concerns and security observations

Possible finger printing of users if this method is accessible without enabling it first.