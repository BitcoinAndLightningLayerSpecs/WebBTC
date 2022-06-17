<template>
  <v-container>
    <v-row>

      <v-col
        class="mb-5"
        cols="3"
      >
        <h2 class="headline font-weight-bold mb-3">
          Action
        </h2>

      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <h2 class="headline font-weight-bold mb-3">
          Bitcoin
        </h2>

      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <h2 class="headline font-weight-bold mb-3">
          WebLN
        </h2>

      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <h2 class="headline font-weight-bold mb-3">
          Proposed
        </h2>

      </v-col>
    </v-row>
    <v-row v-for="item in items" :key="item.name" >
            <v-col
        class="mb-5"
        cols="3"
      >
        <h2>{{item.name}}</h2>
        <p>{{item.description}}</p>
        <p><a :href="item.docs">Docs</a></p>
      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.bitcoin.call()">{{item.name}}</v-btn></p>
        Request: {{item.bitcoin.signature}}
        <div v-show="item.bitcoin.response">
          Response:
          <pre>{{item.bitcoin.response}}</pre>
        </div>

      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.webln.call()">{{item.name}}</v-btn></p>

        <div>
        Request: {{item.webln.signature}}
        <div v-show="item.webln.response">
          Response:
          <pre>{{item.webln.response}}</pre>
        </div>
        </div>
      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.wrapper.call()">{{item.name}}</v-btn></p>
        Request: {{item.wrapper.signature}}
        <div v-show="item.wrapper.response">
        <pre>{{item.wrapper.response}}</pre>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

  class WrapperAPI {
    enable() {
      window.bitcoin.enable();
      window.webln.enable();
    }
  }
  export default {
    name: 'Index',
    mounted () {
      this.api = new WrapperAPI()
    },
    data: () => ({
      items : [{
        name: 'Enable Wallet',
        description: 'Enable wallet API',
        docs: '/docs/enable/',
        bitcoin: {
          signature : "enable()",
          params: '[]',
          response: false,
          call () {
            window.bitcoin.enable().then((data) => {
                this.response = data
            })
          }
        },
        webln: {
          signature : "enable()",
          response : false,
          call () {
            window.webln.enable().then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          response: false,
          signature: "enable()",
          call() {
            this.response = {
              enabled: true
            }
          } 
        }
      },{
        name: 'Wallet Info',
        description: 'Get information',
        docs: '/docs/info/',
        bitcoin: {
          signature: "NA",
          response: false,
          call() {
            this.response = "Not implemented"
          }
        },
        webln: {
          signature: "getInfo()",
          response: false,
          call() {            
            window.webln.getInfo().then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          response: false,
          signature: "getInfo()",
          call() {
            this.response = {
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
          }
        }
      },{
        name: 'Message Signature',
        description: 'Sign a message',
        docs: '/docs/signatures/sign/',
        bitcoin: {
          signature: "signMessage(msg, address)",
          response: false,
          call() {
            window.bitcoin.request({
              method: 'wallet_getAddresses',
              params: [0, 1, false]
            }).then((data) => {
              window.bitcoin.request({
                method: 'wallet_signMessage',
                params: ['Message', data[0].address]
              }).then((data) => {
                this.response = data
              })
            })
          }
        },
        webln: {
          signature: "signMessage(msg)",
          response: false,
          call() {
            window.webln.signMessage("test").then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          response: false,
          signature: "signMessage(msg)",
          call() {
            this.response = "2047ab7b010687146ef9d69648cbdc4610b7ebaf6f21d7255f2113fe87b24d4b4264eef980d21f29d3ba81b369e41bf532b1292021af16c6773187c34d090b7efb"
          }
        }
      },{
        name: 'Verify Message',
        description: 'Verify a message and signature',
        docs: '/docs/signatures/verify/',
        bitcoin: {
          response: false,
          signature: "verifyMessage(signature, msg)",
          call() {
            console.log("Not implemented")
          }
        },
        webln: {
          response: false,
          signature: "verifyMessage(signature, msg)",
          call() {
            window.webln.verifyMessage("d631ou68jhccqn4pnqreijorrpbfkb85durtw1r75uxj8s3b4w5rc718fx36rco7y4wtgjyytk5edhrrc8bgx1afr4oaxs9u983o5kyc", "data").then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          response: false,
          signature: "verifyMessage(signature, msg)",
          call() {
            this.response = true
          }
        }
      },{
        name: 'Invoice',
        description: 'makeInvoice',
        docs: '/docs/invoices/makeInvoice/',
        bitcoin: {
          response: false,
          signature: "makeInvoice(bip21uri)",
          call() {
            window.bitcoin.request({
              method: 'makeInvoice',
              params: ["mpUVDdBihqyMvzDmWwpvWLD92tDebh7ZCV", 10000]
            }).then((data) => {
              this.response = data
            })
          }
        },
        webln: {
          signature: "makeInvoice(amount)",
          call() {
            window.webln.makeInvoice({amount:1}).then(console.log)
          }
        },
        wrapper: {
          response: false,
          signature: "sendPayment(amount)",
          call() {
            this.response = {
              paymentRequest: 'lnbc10n1p3x9thxpp59xj4cmm26jnpnrfekgncyj42e9lxredz…734s07kxt8hl2s6wuv20kh7kw7h5lurtmyscsrwgkgptn4z2j', rHash: '29a55c6f6ad4a6198d39b227824aaac97e61e5a2428db7dab7f8b097ae5d28ca',
              paymentRequestUri: 'bitcoin:address?amount=0&label=Label&message=Message'
            }
          }
        }
      },{
        name: 'Send Payment',
        description: 'sendPayment',
        docs: '/docs/transactions/send/',
        bitcoin: {
          response: false,
          signature: "sendPayment(address, amount)",
          call() {
            window.bitcoin.request({
              method: 'sendPayment',
              params: [""]
            }).then((data) => {
              this.response = data
            })
          }
        },
        webln: {
          signature: "sendPayment(lnInvoice)",
          call() {
            window.webln.sendPayment("lnbcrt10n1pscucp2pp592nxaguujcwgq5fg8v7tlakf9rvxqc9taugdxku0yyeca8ctncrqdqug9kxy7fqd9h8vmmfvdjjqmt9d4hscqzpgxqyz5vqsp579mntt5nzvpylx8nt09a0lkw7k2xyec2ypc8tdzsntz5as53rnls9qyyssqxzmed9es4hmucdlpghrqdzpapmelqw6hmt4c8ed8g4q6nsuu7q0j9glvda6sk8rr0t6mz5x4q9vh0d5y3kk6wwut54f62vdxqhld54gqq6awdj").then(console.log)
          }
        },
        wrapper: {
          response: false,
          signature: "sendPayment(?)",
          call() {
            this.response = {
              "preimage": "6665333431626331363632653134386630643435626532626165383332323333",
              "paymentHash": "d221b791c7ef1996b25424ff7cfb4ddf8d4444076666ce6c4ba0f6a24d99117e",
              "txid":"ba8d75e01ab32932d9ac899418a6bec95f2869e1b1c161b871f661c5a8789a0e"
            }
          }
        }
      },{
        name: 'Addresses',
        description: 'Get Address',
        docs: '/docs/addresses/getAddress/',
        bitcoin: {
          response: false,
          signature: "getAddresses(index, limit, isChange)",
          call() {
            window.bitcoin.request({
              method: 'wallet_getAddresses',
              params: [0, 1, false]
            }).then((data) => {
              this.response = data
            })
          }
        },
        webln: {
          response:false,
          signature: "makeInvoice(sats, label)",
          call() {
            window.webln.makeInvoice(1, "message").then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          response: false,
          signature: "???",
          call() {
            this.response = [{
                address: "tb1qqwn2dp8mundc6mf3xt4c8puqakk0vrcgzdayq2",
                derivationPath: "84'/1'/0'/0/0",
                index: 0
            }, {
                address: "tb1qca6k2ke5jdrwmdqcku4eex4k9hzzzhzshhsgpn",
                derivationPath: "84'/1'/0'/0/1",
                index: 1
            }, {
                address: "tb1q6e36gyc8vhv97k9m2uldndsl8xg80yd49mhqpx",
                derivationPath: "84'/1'/0'/0/2",
                index: 2
            }, {
                address: "tb1qvphc32p0qxl2fm89r04epmtxvdt7l7dl5a955c",
                derivationPath: "84'/1'/0'/0/3",
                index: 3
            }, {
                address: "tb1qxm90ahvjnut9d7mw8d0r22czldnu3kqyef55nn",
                derivationPath: "84'/1'/0'/0/4",
                index: 4
            }, {
                address: "tb1q8wjjk4gu3am2tjg833qulqt69ny8e24vt8ccj6",
                derivationPath: "84'/1'/0'/0/5",
                index: 5
            }, {
                address: "tb1q7jkkn80maps9z068u22jrpv65t9epjlrl4zpzj",
                derivationPath: "84'/1'/0'/0/6",
                index: 6
            }, {
                address: "tb1qrzpw5rrm9w8qf3v3y43av3npeqhgp9lng5xtyk",
                derivationPath: "84'/1'/0'/0/7",
                index: 7
            }, {
                address: "tb1q9vu3j2m6u48sv53g7e24lfx2c9mavv0ee6wr02",
                derivationPath: "84'/1'/0'/0/8",
                index: 8
            }, {
                address: "tb1q0m2f0vjc4njy5d0vzmlwre8jdtar9x9w7nz9jg",
                derivationPath: "84'/1'/0'/0/9",
                index: 9
            }]
          }
        }
      }]
    }),
    methods : {
      enable() {
        this.api.enable()
      }
    }
  }
</script>
<style scoped>
 pre {
    background: #f4f4f4;
    border: 1px solid #ddd;
    border-left: 3px solid #f36d33;
    color: #666;
    page-break-inside: avoid;
    font-family: monospace;
    font-size: 15px;
    line-height: 1.6;
    margin-bottom: 1.6em;
    max-width: 100%;
    overflow: auto;
    padding: 1em 1.5em;
    display: block;
    word-wrap: break-word;
}


</style>