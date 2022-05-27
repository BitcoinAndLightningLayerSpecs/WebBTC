# Send transaction

The `sendTransaction` method is called to make an onchain payment. 

## Syntax

```
sendTransaction(String)
```

## Parameters

- address: String <span class="badge">Required</span>
- amount: String <span class="badge">Required</span>

## Returns

- txid: String 

## Example

```
window.bitcoin.sendTransaction('tb1qqwn2dp8mundc6mf3xt4c8puqakk0vrcgzdayq2', 10000)

"ba8d75e01ab32932d9ac899418a6bec95f2869e1b1c161b871f661c5a8789a0e"
}
```

## Notes

- The purpose of this method includes both signing as well as broadcasting the transaction. The implementation details of this could be done as separate concerns. 
- There are more complex versions for onchain including PSBT, pay multiple addresses at the same time.
