<div align="center" style="text-align: center;">
  <h1 style="border-bottom: none;">lit-ntml</h1>

  <p>Inspired by <a href="https://github.com/PolymerLabs/lit-html" target="_blank" rel="noopener">lit-html</a> but for Node.js.</p>
</div>

<hr />

[![Follow me][follow-me-badge]][follow-me-url]

[![Version][version-badge]][version-url]
[![Node version][node-version-badge]][node-version-url]
[![MIT License][mit-license-badge]][mit-license-url]

[![Downloads][downloads-badge]][downloads-url]
[![Total downloads][total-downloads-badge]][downloads-url]
[![Packagephobia][packagephobia-badge]][packagephobia-url]
[![Bundlephobia][bundlephobia-badge]][bundlephobia-url]

[![CircleCI][circleci-badge]][circleci-url]
[![Dependency Status][daviddm-badge]][daviddm-url]
[![codecov][codecov-badge]][codecov-url]
[![Coverage Status][coveralls-badge]][coveralls-url]

[![codebeat badge][codebeat-badge]][codebeat-url]
[![Codacy Badge][codacy-badge]][codacy-url]
[![Code of Conduct][coc-badge]][coc-url]

> Lightweight and modern templating for SSR in [Node.js][nodejs-url], inspired by [lit-html][lit-html-url].

This module also gets featured in [web-padawan/awesome-lit-html][web-padawan-awesome-lit-html-url]. Make sure to check the repo out for awesome things inspired by [lit-html][lit-html-url]. 👍💯

## Table of contents <!-- omit in toc -->

- [Features](#features)
- [Pre-requisite](#pre-requisite)
- [Enable syntax highlighting when writing HTML with template literal](#enable-syntax-highlighting-when-writing-html-with-template-literal)
  - [Visual Studio Code](#visual-studio-code)
- [Install](#install)
- [Usage](#usage)
  - [TypeScript or native ES Modules](#typescript-or-native-es-modules)
    - [html()](#html)
    - [htmlFragment()](#htmlfragment)
  - [Node.js](#nodejs)
    - [html()](#html-1)
    - [htmlFragment()](#htmlfragment-1)
    - [SSR with Express (Node.js)](#ssr-with-express-nodejs)
  - [Browser](#browser)
    - [ES Modules](#es-modules)
    - [UMD](#umd)
- [deno](#deno)
- [API Reference](#api-reference)
  - [html()](#html-2)
  - [htmlFragment()](#htmlfragment-2)
- [License](#license)

## Features

- [x] `await` all tasks including Functions, Promises, and whatnot.
- [x] Compatible for ES Modules (`import { html } from 'lit-ntml'`) and CommonJS (`const { html } = require('lit-ntml');`).
- [x] Parses `PromiseList` or `List` by default, without explicit joining.
- [x] Support HTML syntax highlighting + autocompletion with [vscode-lit-html][vscode-lit-html-url] in JavaScript's template string.
- [x] Support native ES Module via `.mjs`.

## Pre-requisite

- [Node.js][nodejs-url] >= 10.18.1
- [NPM][npm-url] >= 6.13.4 ([NPM][npm-url] comes with [Node.js][nodejs-url] so there is no need to install separately.)

## Enable syntax highlighting when writing HTML with template literal

### Visual Studio Code

1. Install [vscode-lit-html][vscode-lit-html-url] extension.
2. If the extension does not provide that syntax highlighting and autocompletion, try writing your templates in `.jsx` file (or `.tsx` file if you're [TypeScript][typescript-url] user) . That should work.

## Install

```sh
# Install via NPM
$ npm install lit-ntml
```

## Usage

### TypeScript or native ES Modules

#### html()

```ts
import { html } from 'lit-ntml';

const peopleList = ['Cash Black', 'Vict Fisherman'];
const syncTask = () => `<h1>Hello, World!</h1>`;
const asyncLiteral = Promise.resolve('<h2>John Doe</h2>');
const asyncListTask = async () => `<ul>${peopleList.map(n => `<li>${n}</li>`)}</ul>`;

/** Assuming top-level await is enabled... */
await html`${syncTask}${asyncLiteral}${asyncListTask}`; /** <!DOCTYPE html><html><head></head><body><h1>Hello, World!</h1><h2>John Doe</h2><ul><li>Cash Black</li><li>Vict Fisherman</li></ul></body></html> */
```

#### htmlFragment()

```ts
import { htmlFragment as html } from 'lit-ntml';

const syncTask = () => `<h1>Hello, World!</h1>`;
const externalStyleLiteral = `<style>body { margin: 0; padding: 0; box-sizing: border-box; }</style>`;

/** Assuming top-level await is enabled... */
await html`${externalStyleLiteral}${syncTask}`; /** <style>body { margin: 0; padding: 0; box-sizing: border-box; }</style><h1>Hello, World!</h1> */
```

### Node.js

#### html()

```js
const { html } = require('lit-ntml');

const peopleList = ['Cash Black', 'Vict Fisherman'];
const syncTask = () => `<h1>Hello, World!</h1>`;
const asyncLiteral = Promise.resolve('<h2>John Doe</h2>');
const asyncListTask = async () => `<ul>${peopleList.map(n => `<li>${n}</li>`)}</ul>`;

/** Assuming top-level await is enabled... */
await html`${syncTask}${asyncLiteral}${asyncListTask}`; /** <!DOCTYPE html><html><head></head><body><h1>Hello, World!</h1><h2>John Doe</h2><ul><li>Cash Black</li><li>Vict Fisherman</li></ul></body></html> */
```

#### htmlFragment()

```js
const { htmlFragment } = require('lit-ntml');

const html = htmlFragment;
const syncTask = () => `<h1>Hello, World!</h1>`;
const externalStyleLiteral = `<style>body { margin: 0; padding: 0; box-sizing: border-box; }</style>`;

/** Assuming top-level await is enabled... */
await html`${externalStyleLiteral}${syncTask}`; /** <style>body { margin: 0; padding: 0; box-sizing: border-box; }</style><h1>Hello, World!</h1> */
```

#### SSR with Express (Node.js)

[![Edit SSR with Express and LitNtml](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/ssr-with-express-and-litntml-4tbv9?fontsize=14)

### Browser

#### ES Modules

```html
<!doctype html>
<html>
  <head>
    <script type="module">
      import { html } from 'https://unpkg.com/lit-ntml@latest/dist/lit-ntml.min.js';

      // --snip
    </script>
  </head>
</html>
```

#### UMD

```html
<!doctype html>
<html>
  <head>
    <script src="https://unpkg.com/lit-ntml@latest/dist/lit-ntml.umd.min.js"></script>
    <script>
      var { html } = window.LitNtml;

      // --snip
    </script>
  </head>
</html>
```

## deno

👉 Check out the [deno][] module at [deno_mod/lit_ntml][].

## API Reference

### html()

- returns: <[Promise][promise-mdn-url]&lt;[string][string-mdn-url]&gt;> Promise which resolves with rendered HTML document string.

### htmlFragment()

- returns: <[Promise][promise-mdn-url]&lt;[string][string-mdn-url]&gt;> Promise which resolves with rendered HTML document fragment string.

## License

[MIT License](https://motss.mit-license.org) © Rong Sen Ng

<!-- References -->
[nodejs-url]: https://nodejs.org
[lit-html-url]: https://github.com/PolymerLabs/lit-html
[npm-url]: https://www.npmjs.com
[parse5-url]: https://www.npmjs.com/package/parse5
[pretty-url]: https://www.npmjs.com/package/pretty
[vscode-lit-html-url]: https://github.com/mjbvz/vscode-lit-html
[typescript-url]: https://github.com/Microsoft/TypeScript
[htmlminifier-url]: https://github.com/kangax/html-minifier
[htmlminifier-flags-url]: https://github.com/kangax/html-minifier#options-quick-reference
[pretty-flag-url]: https://github.com/jonschlinkert/pretty#ocd
[web-padawan-awesome-lit-html-url]:
 https://github.com/web-padawan/awesome-lit-html
[deno]: https://github.com/denoland/deno
[deno_mod/lit_ntml]: https://github.com/motss/deno_mod/tree/master/lit_ntml

[parse-promiselist-or-list-url]: #parse-promiselist-or-list
[ntmlopts-url]: #ntmlopts
[default-minify-options-url]: #default_minify_options

<!-- MDN -->
[map-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
[string-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[object-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
[number-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[boolean-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[html-style-element-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/API/HTMLStyleElement
[promise-mdn-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

<!-- Badges -->
[follow-me-badge]: https://flat.badgen.net/twitter/follow/igarshmyb?icon=twitter


[version-badge]: https://flat.badgen.net/npm/v/lit-ntml?icon=npm
[node-version-badge]: https://flat.badgen.net/npm/node/lit-ntml
[mit-license-badge]: https://flat.badgen.net/npm/license/lit-ntml

[downloads-badge]: https://flat.badgen.net/npm/dm/lit-ntml
[total-downloads-badge]: https://flat.badgen.net/npm/dt/lit-ntml?label=total%20downloads
[packagephobia-badge]: https://flat.badgen.net/packagephobia/install/lit-ntml
[bundlephobia-badge]: https://flat.badgen.net/bundlephobia/minzip/lit-ntml

[circleci-badge]: https://flat.badgen.net/circleci/github/motss/lit-ntml?icon=circleci
[daviddm-badge]: https://flat.badgen.net/david/dep/motss/lit-ntml
[codecov-badge]: https://flat.badgen.net/codecov/c/github/motss/lit-ntml?label=codecov&icon=codecov
[coveralls-badge]: https://flat.badgen.net/coveralls/c/github/motss/lit-ntml?label=coveralls

[codebeat-badge]: https://codebeat.co/badges/46b91b60-804d-4909-a647-1784ae283f19
[codacy-badge]: https://api.codacy.com/project/badge/Grade/bb0c739bc5144a8b80197f3fa3bb2273
[coc-badge]: https://flat.badgen.net/badge/code%20of/conduct/pink

<!-- Links -->
[follow-me-url]: https://twitter.com/igarshmyb?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=motss/lit-ntml

[version-url]: https://www.npmjs.com/package/lit-ntml
[node-version-url]: https://nodejs.org/en/download
[mit-license-url]: https://github.com/motss/lit-ntml/blob/master/LICENSE

[downloads-url]: http://www.npmtrends.com/lit-ntml
[packagephobia-url]: https://packagephobia.now.sh/result?p=lit-ntml
[bundlephobia-url]: https://bundlephobia.com/result?p=lit-ntml

[circleci-url]: https://circleci.com/gh/motss/lit-ntml/tree/master
[daviddm-url]: https://david-dm.org/motss/lit-ntml
[codecov-url]: https://codecov.io/gh/motss/lit-ntml
[coveralls-url]: https://coveralls.io/github/motss/lit-ntml?branch=master

[codebeat-url]: https://codebeat.co/projects/github-com-motss-lit-ntml-master
[codacy-url]: https://www.codacy.com/app/motss/lit-ntml?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=motss/lit-ntml&amp;utm_campaign=Badge_Grade
[coc-url]: https://github.com/motss/lit-ntml/blob/master/code-of-conduct.md
