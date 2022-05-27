# Send Payment

The `sendPayment` method is called to pay an lightning invoice or BIP21 URI.

## Syntax

```
sendPayment(String)
```

## Parameters

- bip21 url : string  or paymentRequest: string <span class="badge">Required</span>

## Returns

- Promise

> **_NOTE:_**  
This call is asynchronus is would return a promise based on wether or not the payment has been broadcast <span class="badge">Onchain</span> and or processed successfully <span class="badge">WebLN</span>.

## Example

```
// Example for processing a BIP21 URI Invoice
> await window.webbtc.sendPayment('bitcoin:n1nk1j5DKmmWWuV2TvzhUb3AYBtnqAK1u1?amount=1')
{
  "txid":"ba8d75e01ab32932d9ac899418a6bec95f2869e1b1c161b871f661c5a8789a0e"
}
```


```
// Example for processing a LN payment
window.webbtc.sendPayment('lnbc10n1p3x9thxpp59xj4cmm26jnpnrfekgncyj42e9lxredz…734s07kxt8hl2s6wuv20kh7kw7h5lurtmyscsrwgkgptn4z2j')

{
  "preimage": "6665333431626331363632653134386630643435626532626165383332323333",
  "paymentHash": "d221b791c7ef1996b25424ff7cfb4ddf8d4444076666ce6c4ba0f6a24d99117e"
}
```

## Notes

- The purpose of this method includes both signing as well as broadcasting the transaction. The implementation details of this could be done as separate concerns. 
- There are more complex versions for onchain including PSBT, pay multiple addresses at the same time.
