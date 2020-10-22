Node-config with dynamic configuration
======================================
You don't have to restart your Node.js app to apply new configuration. Simply update the configuration files. This repository is forked from [lorenwest/node-config](https://github.com/lorenwest/node-config) and more specifically this [Pull Request](https://github.com/lorenwest/node-config/pull/621#issuecomment-712556170).

Quick Start
---------------
**Install in your app directory, and edit the default config file.**

```shell
$ npm install config-dynamic
$ mkdir config
$ vi config/default.json
```
```js
{
  // Customer module configs
  "foo": {
    "bar": "fizz"
  }
}
```

**Example express server that returns the config value:**
```shell
$ npm install express
$ touch index.js
```
```js 
const config = require('config')
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  const dbConfig = config.get('foo.bar')
  console.log(dbConfig) // Display the updated configuration
  res.send(dbConfig)
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

**Start your app server:**
```shell
$ node index.js
Example app listening at http://localhost:3000
```

**Poll the server for the latest configuration:**
```shell
$ curl localhost:3000
fizz
```
**Update config/default.json.**
```js
{
  // Customer module configs
  "foo": {
    "bar": "buzz"
  }
}
```
**Poll the server for the latest configuration:**
```shell
$ curl localhost:3000
buzz
```

License
-------
May be freely distributed under the [MIT license](https://raw.githubusercontent.com/lorenwest/node-config/master/LICENSE).



