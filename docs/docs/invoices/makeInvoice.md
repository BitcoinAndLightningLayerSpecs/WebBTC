# Create a new invoice

The `makeInvoice` method is used to generate a new invoice.

## Syntax

```
makeInvoice(Object)
```

## Parameters

  - Object
    - amount : string | number <span class="badge">Optional</span>
    - defaultMemo : string <span class="badge">Optional</span>
    - label : string <span class="badge">Optional</span>
    - message : string <span class="badge">Optional</span>

> **_NOTE:_**  
  Providing any of the above would result in a pre-populating a a prompt which requires the user to complete the rest of the information.
  e.g. Only providing the amount parameter might result in the following prompt.
  
  <img src="/assets/makeinvoice.png" style="width:200px;"/>

## Returns

  - Object
    - paymentRequest: string; <span class="badge">LN Invoice</span>
    - BIP21 address string; <span class="badge">Onchain BIP 21 URI</span>


## Example

```
await window.webln.makeInvoice({})
  {
    paymentRequest: 'lnbc10n1p3x9thxpp59xj4cmm26jnpnrfekgncyj42e9lxredz…734s07kxt8hl2s6wuv20kh7kw7h5lurtmyscsrwgkgptn4z2j', rHash: '29a55c6f6ad4a6198d39b227824aaac97e61e5a2428db7dab7f8b097ae5d28ca'
  }
```

```
window.bitcoin.makeInvoice({amount:1, label: 'Label', message: 'Message'})

bitcoin:address?amount=0&label=Label&message=Message
```

## Considerations

These parameters might not be required in the spec as they are used by the website for convenience purposes in setting up the invoice dialog.

defaultAmount?: string | number;
minimumAmount?: string | number;
maximumAmount?: string | number;

## Notes

The amount parameter doesn't distinguish between bitcoin and satoshis


## Reference

https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki

```
bitcoinurn     = "bitcoin:" bitcoinaddress [ "?" bitcoinparams ]
bitcoinaddress = *base58
bitcoinparams  = bitcoinparam [ "&" bitcoinparams ]
bitcoinparam   = [ amountparam / labelparam / messageparam / otherparam / reqparam ]
amountparam    = "amount=" *digit [ "." *digit ]
labelparam     = "label=" *qchar
messageparam   = "message=" *qchar
otherparam     = qchar *qchar [ "=" *qchar ]
reqparam       = "req-" qchar *qchar [ "=" *qchar ]
```

## Invoice address description
[Invoice Address](https://en.bitcoin.it/wiki/Invoice_address)
[Meno proposal](https://github.com/lightning/blips/pull/11/files?short_path=1efcc79#diff-1efcc7957e02dad2d5a9deea7032635c9f19100d5a7ee08be166cb1dc9b4d690)
[Payment Requests](https://doc.clickup.com/18307877/d/h/hept5-1721/f06e5c5e4eba551/hept5-421)

Separate Meno into name and description

Label = The who
Message = The what