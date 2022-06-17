# Extendability

There is room for extending this API through a request method. This method might also be useful as a base from which all the other methods in the specification might have wrapper methods. 

## Syntax

```
window.webbtc.request(method, params)
```


## Parameters

- method: String <span class="badge">Required</span>
- params: Array <span class="badge">Required</span>

## Returns

- Promise | Object

> **_NOTE:_**  
This call might be asynchronous is would return a promise based on wether or not the payment has been broadcast <span class="badge">Onchain</span> and or processed successfully 

## Example

```
// Example of calling an existing method
window.webbtc.request('getInfo',[])
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

```
// Example for calling an arbitrary message not covered in the specification

// Custom method might be 
// hello(name) {
// return "Hello ${name}" 
//}

> await window.webbtc.request('hello',['Alice'])

Hello Alice
```

