# torus-client
Torus REST and RPC client

## Installation

Install the package via `yarn`:

```sh
yarn add https://github.com/sskender/torus-client
```

or via `npm`:

Install the package via `npm`:

```sh
npm install --save https://github.com/sskender/torus-client
```

## Usage
### Client(...args)
#### Arguments
1. `[agentOptions]` _(Object)_: Optional `agent` [options](https://github.com/request/request#using-optionsagentoptions) to configure SSL/TLS.
2. `[headers=false]` _(boolean)_: Whether to return the response headers.
3. `[host=localhost]` _(string)_: The host to connect to.
4. `[logger=debugnyan('torus-client')]` _(Function)_: Custom logger (by default, `debugnyan`).
5. `[network=mainnet]` _(string)_: The network.
6. `[password]` _(string)_: The RPC server user password.
7. `[port=22411]` _(string)_: The RPC server port.
8. `[ssl]` _(boolean|Object)_: Whether to use SSL/TLS with strict checking (_boolean_) or an expanded config (_Object_).
9. `[ssl.enabled]` _(boolean)_: Whether to use SSL/TLS.
10. `[ssl.strict]` _(boolean)_: Whether to do strict SSL/TLS checking (certificate must match host).
11. `[timeout=30000]` _(number)_: How long until the request times out (ms).
12. `[username]` _(number)_: The RPC server user name.
13. `[version]` _(string)_: Which version to check methods for.
14. `[wallet]` _(string)_: Which wallet to manage.

### Examples

#### Basic client settings

```js
const client = new Client({
  host: '127.0.0.1',
  password: 'somepassword',
  port: 22411,
  username: 'someusername'
 });
```

#### Connecting to an SSL/TLS server with strict checking enabled
By default, when `ssl` is enabled, strict checking is implicitly enabled.

```js
const fs = require('fs');
const client = new Client({
  agentOptions: {
    ca: fs.readFileSync('/etc/ssl/torusd/cert.pem')
  },
  ssl: true
});
```

#### Connecting to an SSL/TLS server without strict checking enabled

```js
const client = new Client({
  ssl: {
    enabled: true,
    strict: false
  }
});
```

#### Using promises to process the response

```js
client.getBalance().then((bal) => console.log(bal));
```

### Floating point number precision in JavaScript

Due to [JavaScript's limited floating point precision](http://floating-point-gui.de/), all big numbers (numbers with more than 15 significant digits) are returned as strings to prevent precision loss. This includes both the RPC and REST APIs.

## License
MIT
