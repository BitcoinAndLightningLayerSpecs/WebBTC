# WebBTC 

A common convention in the Bitcoin web application ecosystem is for key management software (“wallets”) to expose their API via a JavaScript object in the web page. This object is called the common web wallet interface.

Historically, Provider implementations have exhibited conflicting interfaces and behaviors between wallets. This working group formalizes an Bitcoin extension API to promote wallet interoperability. The API is designed to be minimal, event-driven, and agnostic of transport and RPC protocols. Its functionality is easily extended by defining new RPC methods and message event types.

Historically, providers have been made available as `window.bitcoin` or `window.webln` in web browsers, but this convention is not part of the specification.

A list of current work in progress can be tracked from the [issues](https://github.com/BitcoinAndLightningLayerSpecs/WebBTC/issues) tab in the [playground repository](https://github.com/BitcoinAndLightningLayerSpecs/WebBTC/issues), which includes a functional spec demonstration. A hosted instance of the demo can be found [here](hhttps://bitcoinandlightninglayerspecs.github.io/) together with the accompanying [specification documentation](hhttps://bitcoinandlightninglayerspecs.github.io/docs).

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

For documentation see [docs](docs)
