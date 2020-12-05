# 👂 listhen

> Elegant http listener

[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![Github Actions][github-actions-src]][github-actions-href]
[![Codecov][codecov-src]][codecov-href]

✔️ Promisified interface for listening and closing server

✔️ Works with express/connect or plain http handle function

✔️ Support HTTP and HTTPS

✔️ URL Generator utility (useful for tests)

✔️ Automatically assign a port or fallback to human friendly alternative (with [get-port-please](https://github.com/nuxt-contrib/get-port-please))

✔️ Automatically generate listening URL and show on console

✔️ Automatically copy URL to clipboard

✔️ Automatically open in browser (opt-in)

✔️ Automatically generate self signed certificate

✔️ Automatically detect test and production environments

✔️ Automatically close with process shutdown signal

## Install

Install using npm or yarn:

```bash
npm i listhen
# or
yarn add listhen
```

Import into your Node.js project:

```js
// CommonJS
const { listen } = require('listhen')

// ESM
import { listen } from 'listhen'
```

## Usage

**Function signuture:**

```ts
const { url, getURL, server, close } = await listen(handle, options?)
```

**Plain handle function:**

```ts
listen('/', ((_req, res) => {
  res.end('hi')
})
```

**With express/connect:**

```ts
const express = require('express')
const app = express()

app.use('/', ((_req, res) => {
  res.end('hi')
})

listen(app)
```

## Options

### `name`

- Default: `'server'`

Instance name used for CLI message.

### `port`

- Default: `process.env.PORT` or 3000 or memorized random (see [get-port-please](https://github.com/nuxt-contrib/get-port-please))

Port to listen.

### `https`

- Default: `false`

Listen with `https` protocol. By default uses a self-signed certificated.

### `cetificate`

Path to https certificate files `{ key, cert }`

### `selfsigned`

Options for self-signed certificate (see [selfsigned](https://github.com/jfromaniello/selfsigned)).

### `showURL`

- Default: `true` (force disabled on test environment)

Show a CLI message for listening URL.

### `baseURL`

- Default: `/`

### `open`

- Default: `false` (force disabled on test and production environments)

Open URL in browser. Silently ignores errors.

### `clipboard`

- Default: `true` (force disabled on test and production environments)

Copy URL to clipboard. Silently ignores errors.

### `isTest`

- Default: `process.env.NODE_ENV === 'test'`

Detect if running in a test environment to disable some features.

### `autoClose`

- Default: `true`

Automatically close when an exit signal is recieved on process.

### `autoCloseSignals`

- Default: `['exit', 'SIGINT', 'SIGUSR1', 'SIGUSR2', 'SIGTERM']`

Signals to auto close.

## License

MIT. Made with 💖

<!-- Badges -->
[npm-version-src]: https://img.shields.io/npm/v/listhen?style=flat-square
[npm-version-href]: https://npmjs.com/package/listhen

[npm-downloads-src]: https://img.shields.io/npm/dm/listhen?style=flat-square
[npm-downloads-href]: https://npmjs.com/package/listhen

[github-actions-src]: https://img.shields.io/github/workflow/status/nuxt-contrib/listhen/ci/main?style=flat-square
[github-actions-href]: https://github.com/nuxt-contrib/listhen/actions?query=workflow%3Aci

[codecov-src]: https://img.shields.io/codecov/c/gh/nuxt-contrib/listhen/main?style=flat-square
[codecov-href]: https://codecov.io/gh/nuxt-contrib/listhen
