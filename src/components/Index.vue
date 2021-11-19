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
      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.bitcoin.call()">{{item.name}}</v-btn></p>
        Requet: {{item.bitcoin.signature}}
        <div v-show="item.bitcoin.response">
          Response:
          <pre>
            {{item.bitcoin.response}}
          </pre>
        </div>

      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.webln.call()">{{item.name}}</v-btn></p>

        <div>
        Requet: {{item.webln.signature}}
        <div v-show="item.webln.response">
          Response:
          <pre>
            {{item.webln.response}}
          </pre>
        </div>
        </div>
      </v-col>

      <v-col
        class="mb-5"
        cols="3"
      >
        <p><v-btn @click="item.wrapper.call()">{{item.name}}</v-btn></p>
        Requet: {{item.wrapper.signature}}
        <div v-show="item.wrapper.response">
        <pre>
          {{item.wrapper.signature}}
        </pre>
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
          signature: "enable()",
          call() {
            this.bitcoin.call()
            this.webln.call()
          } 
        }
      },{
        name: 'Wallet Info',
        description: 'Get information',
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
            window.webln.getInfo().then((data,r) => {
              console.log(data,r )
              this.response = data
            })
          }
        },
        wrapper: {
          signature: "getInfo()",
          call() {
            this.bitcoin.call()
            this.webln.call()
          }
        }
      },{
        name: 'Message Signature',
        description: 'Sign a message',
        bitcoin: {
          signature: "signMessage()",
          response: false,
          call() {
            window.bitcoin.request({
              method: 'wallet_getAddresses',
              params: [0, 1, false]
            }).then((data) => {
              window.bitcoin.request({
                method: 'wallet_signMessage',
                params: ['x', data[0].address]
              }).then((data) => {
                this.response = data
              })
            })
          }
        },
        webln: {
          signature: "signMessage()",
          response: false,
          call() {
            window.webln.signMessage("test").then((data) => {
              this.response = data
            })
          }
        },
        wrapper: {
          signature: "signMessage()",
          call() {
            this.bitcoin()
            this.webln()
          }
        }
      },{
        name: 'Verify Message',
        description: 'Verify a message and signature',
        bitcoin: {
          signature: "verifyMessage()",
          call() {
            console.log("Not implemented")
          }
        },
        webln: {
          signature: "verifyMessage()",
          call() {
            window.webln.verifyMessage("d631ou68jhccqn4pnqreijorrpbfkb85durtw1r75uxj8s3b4w5rc718fx36rco7y4wtgjyytk5edhrrc8bgx1afr4oaxs9u983o5kyc", "data").then(console.log)
          }
        },
        wrapper: {
          signature: "verifyMessage()",
          call() {
            this.bitcoin()
            this.webln()
          }
        }
      },{
        name: 'Payment',
        description: 'makeInvoice / sendTransaction',
        bitcoin: {
          signature: "sendTransaction()",
          call() {
            window.bitcoin.request({
              method: 'wallet_sendTransaction',
              params: ["mpUVDdBihqyMvzDmWwpvWLD92tDebh7ZCV",10000]
            }).then(console.log)
          }
        },
        webln: {
          signature: "sendPayment()",
          call() {
            window.webln.sendPayment("lnbcrt10n1pscucp2pp592nxaguujcwgq5fg8v7tlakf9rvxqc9taugdxku0yyeca8ctncrqdqug9kxy7fqd9h8vmmfvdjjqmt9d4hscqzpgxqyz5vqsp579mntt5nzvpylx8nt09a0lkw7k2xyec2ypc8tdzsntz5as53rnls9qyyssqxzmed9es4hmucdlpghrqdzpapmelqw6hmt4c8ed8g4q6nsuu7q0j9glvda6sk8rr0t6mz5x4q9vh0d5y3kk6wwut54f62vdxqhld54gqq6awdj").then(console.log)
          }
        },
        wrapper: {
          signature: "xxx()",
          call() {
            this.bitcoin()
            this.webln()
          }
        }
      },{
        name: 'Addresses',
        description: 'Get Address',
        bitcoin: {
          signature: "getAddresses(0, 1, false)",
          call() {
            window.bitcoin.request({
              method: 'wallet_getAddresses',
              params: [0, 1, false]
            }).then(console.log)
          }
        },
        webln: {
          signature: "makeInvoice(1,'Message')",
          call() {
            window.webln.makeInvoice(1, "message")
          }
        },
        wrapper: {
          signature: "xxx",
          call() {
            this.bitcoin()
            this.webln()
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