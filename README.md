# array.prototype.at <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![Build Status][travis-svg]][travis-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ESnext spec-compliant `Array.prototype.at` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the proposed [spec](https://tc39.es/proposal-item-method/).

Because `Array.prototype.at` depends on a receiver (the `this` value), the main export takes the array to operate on as the first argument.

## Getting started

```sh
npm install --save array.prototype.at
```

## Usage/Examples

```js
var at = require('array.prototype.at');
var assert = require('assert');

var arr = [1, [2], [], 3];

var results = at(arr, function (x, i) {
	assert.equal(x, arr[i]);
	return x;
});

assert.deepEqual(results, [1, 2, 3]);
```

```js
var at = require('array.prototype.at');
var assert = require('assert');
/* when Array#at is not present */
delete Array.prototype.at;
var shimmedFlatMap = at.shim();

var mapper = function (x) { return [x, 1]; };

assert.equal(shimmedFlatMap, at.getPolyfill());
assert.deepEqual(arr.at(mapper), at(arr, mapper));
```

```js
var at = require('array.prototype.at');
var assert = require('assert');
/* when Array#at is present */
var shimmedIncludes = at.shim();

var mapper = function (x) { return [x, 1]; };

assert.equal(shimmedIncludes, Array.prototype.at);
assert.deepEqual(arr.at(mapper), at(arr, mapper));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/array.prototype.at
[npm-version-svg]: http://versionbadg.es/es-shims/Array.prototype.at.svg
[travis-svg]: https://travis-ci.org/es-shims/Array.prototype.at.svg
[travis-url]: https://travis-ci.org/es-shims/Array.prototype.at
[deps-svg]: https://david-dm.org/es-shims/Array.prototype.at.svg
[deps-url]: https://david-dm.org/es-shims/Array.prototype.at
[dev-deps-svg]: https://david-dm.org/es-shims/Array.prototype.at/dev-status.svg
[dev-deps-url]: https://david-dm.org/es-shims/Array.prototype.at#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/array.prototype.at.png?downloads=true&stars=true
[license-image]: http://img.shields.io/npm/l/array.prototype.at.svg
[license-url]: LICENSE
[downloads-image]: http://img.shields.io/npm/dm/array.prototype.at.svg
[downloads-url]: http://npm-stat.com/charts.html?package=array.prototype.at
