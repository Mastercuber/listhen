# 👂 listhen

[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![Codecov][codecov-src]][codecov-href]
[![License][license-src]][license-href]
[![JSDocs][jsdocs-src]][jsdocs-href]

Elegant HTTP listener!

[👉 Online Playground](https://stackblitz.com/github/unjs/listhen/tree/main/playground?startScript=dev)

## Features

✅ Dev Server with HMR, Static and Typescript Support (with [unjs/jiti](https://github.com/unjs/jiti))

✅ Works with Node.js, Express, Connect and [unjs/h3](https://github.com/unjs/h3) out of the box

✅ HTTPS support with self-signed certificates

✅ Assign a port or fallback to human friendly fallback (with [unjs/get-port-please](https://github.com/unjs/get-port-please))

✅ Copy URL to Clipboard

✅ Open URL in Browser

✅ Detect test and production environments to auto adjust behavior

✅ Close on exit signal

✅ Gracefully shutdown server with [http-shutdown](https://github.com/thedillonb/http-shutdown)

✅ Show QR Code of Public URL (with [unjs/uqr](https://github.com/unjs/uqr))

## Quick Usage (CLI)

You can run your applications in localhost with typescript support and watch mode using `listhen` CLI:

Create `index.ts`:

```ts
export default (req, res) => {
  res.end("Hello World!");
};
```

or using [unjs/h3](https://github.com/unjs/h3):

```ts
import { createApp, eventHandler } from "h3";

export const app = createApp();

app.use("/", () => "Hello world!");
```

or use npx to invoke `listhen` command:

```sh
npx listhen -w ./index.ts
```

## Usage (API)

Install package:

```bash
# pnpm
pnpm i listhen

# npm
npm i listhen

# yarn
yarn add listhen

```

Import into your Node.js project:

```js
// CommonJS
const { listen, listenAndWatch } = require("listhen");

// ESM
import { listen, listenAndWatch } from "listhen";
```

```ts
const handler = (req, res) => {
  res.end("Hi!")
}

// listener: { url, getURL, server, close, ... }
const listener = await listen(handle, options?)
```

## Options

### `port`

- Default: `process.env.PORT` or 3000 or memorized random (see [get-port-please](https://github.com/unjs/get-port-please))

Port to listen.

### `hostname`

- Default: `process.env.HOST || '0.0.0.0'`

Default hostname to listen.

### `https`

- Type: Boolean | Object
- Default: `false`

Listen on https with SSL enabled.

#### Self Signed Certificate

By setting `https: true`, listhen will use an auto generated self-signed certificate.

You can set https to an object for custom options. Possible options:

- `domains`: (Array) Default is `['localhost', '127.0.0.1', '::1']`.
- `validityDays`: (Number) Default is `1`.

#### User Provided Certificate

Set `https: { cert, key }` where cert and key are path to the ssl certificates.
With an encrypted private key you also need to set `passphrase` on the `https` object.

To provide a certificate stored in a keystore set `https: { pfx }` with a path to the keystore.
When the keystore is password protected also set `passphrase`.

You can also provide inline cert and key instead of reading from filesystem. In this case, they should start with `--`.

### `showURL`

- Default: `true` (force disabled on test environment)

Show a CLI message for listening URL.

### `baseURL`

- Default: `/`

### `open`

- Default: `false` (force disabled on test and production environments)

Open URL in browser. Silently ignores errors.

### `clipboard`

- Default: `false` (force disabled on test and production environments)

Copy URL to clipboard. Silently ignores errors.

### `isTest`

- Default: `process.env.NODE_ENV === 'test'`

Detect if running in a test environment to disable some features.

### `autoClose`

- Default: `true`

Automatically close when an exit signal is received on process.

### `publicURL`

- Default: (the first public URL listening)

The public URL to show in CLI output

### `qr`

- Default: `true`

Print QR Code for public address.

### `public`

- Default: `false` for development or when `hostname` is `localhost` and `true` for production

When enabled, listhen tries to listen to all network interfaces. You can also enable this option using `--host` CLI flag.

## License

MIT. Made with 💖

<!-- Badges -->

[npm-version-src]: https://img.shields.io/npm/v/listhen?style=flat&colorA=18181B&colorB=F0DB4F
[npm-version-href]: https://npmjs.com/package/listhen
[npm-downloads-src]: https://img.shields.io/npm/dm/listhen?style=flat&colorA=18181B&colorB=F0DB4F
[npm-downloads-href]: https://npmjs.com/package/listhen
[codecov-src]: https://img.shields.io/codecov/c/gh/unjs/listhen/main?style=flat&colorA=18181B&colorB=F0DB4F
[codecov-href]: https://codecov.io/gh/unjs/listhen
[license-src]: https://img.shields.io/github/license/unjs/listhen.svg?style=flat&colorA=18181B&colorB=F0DB4F
[license-href]: https://github.com/unjs/listhen/blob/main/LICENSE
[jsdocs-src]: https://img.shields.io/badge/jsDocs.io-reference-18181B?style=flat&colorA=18181B&colorB=F0DB4F
[jsdocs-href]: https://www.jsdocs.io/package/listhen
