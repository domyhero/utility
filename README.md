# utility

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][codecov-image]][codecov-url]
[![npm download][download-image]][download-url]
[![Dependency Status][dependency-image]][dependency-url]
[![devDependency Status][devDependency-image]][devDependency-url]

[npm-image]: https://img.shields.io/npm/v/utility.svg?style=flat-square
[npm-url]: https://npmjs.org/package/utility
[travis-image]: https://img.shields.io/travis/node-modules/utility.svg?style=flat-square
[travis-url]: https://travis-ci.org/node-modules/utility
[codecov-image]: https://codecov.io/github/node-modules/utility/coverage.svg?branch=master
[codecov-url]: https://codecov.io/github/node-modules/utility?branch=master
[download-image]: https://img.shields.io/npm/dm/utility.svg?style=flat-square
[download-url]: https://npmjs.org/package/utility
[dependency-image]: https://david-dm.org/node-modules/utility.svg
[dependency-url]: https://david-dm.org/node-modules/utility
[devDependency-image]: https://david-dm.org/node-modules/utility/dev-status.svg
[devDependency-url]: https://david-dm.org/node-modules/utility#info=devDependencies

A collection of useful utilities.

## Install

```bash
$ npm install utility
```

## Usage

```js
const utils = require('utility');
```

### md5

```js
utils.md5('苏千').should.equal('5f733c47c58a077d61257102b2d44481');
utils.md5(new Buffer('苏千')).should.equal('5f733c47c58a077d61257102b2d44481');
// md5 base64 format
utils.md5('苏千', 'base64'); // 'X3M8R8WKB31hJXECstREgQ=='

// Object md5 hash. Sorted by key, and JSON.stringify. See source code for detail
utils.md5({foo: 'bar', bar: 'foo'}).should.equal(utils.md5({bar: 'foo', foo: 'bar'}));
```

### sha1

```js
utils.sha1('苏千').should.equal('0a4aff6bab634b9c2f99b71f25e976921fcde5a5');
utils.sha1(new Buffer('苏千')).should.equal('0a4aff6bab634b9c2f99b71f25e976921fcde5a5');
// sha1 base64 format
utils.sha1('苏千', 'base64'); // 'Ckr/a6tjS5wvmbcfJel2kh/N5aU='

// Object sha1 hash. Sorted by key, and JSON.stringify. See source code for detail
utils.sha1({foo: 'bar', bar: 'foo'}).should.equal(utils.sha1({bar: 'foo', foo: 'bar'}));
```

### sha256

```js
utils.sha256(new Buffer('苏千')).should.equal('75dd03e3fcdbba7d5bec07900bae740cc8e361d77e7df8949de421d3df5d3635');
```

### hmac

```js
// hmac-sha1 with base64 output encoding
utils.hmac('sha1', 'I am a key', 'hello world'); // 'pO6J0LKDxRRkvSECSEdxwKx84L0='
```

### decode and encode

```js
// base64 encode
utils.base64encode('你好￥'); // '5L2g5aW977+l'
utils.base64decode('5L2g5aW977+l') // '你好￥'

// urlsafe base64 encode
utils.base64encode('你好￥', true); // '5L2g5aW977-l'
utils.base64decode('5L2g5aW977-l', true); // '你好￥'

// html escape
utils.escape('<script/>"& &amp;'); // '&lt;script/&gt;&quot;&amp; &amp;'

// Safe encodeURIComponent and decodeURIComponent
utils.decodeURIComponent(utils.encodeURIComponent('你好, nodejs')).should.equal('你好, nodejs');
```

### others

___[WARNNING] getIP() remove, PLEASE use `https://github.com/node-modules/address` module instead.___

```js
// get a function parameter's names
utils.getParamNames(function (key1, key2) {}); // ['key1', 'key2']

// get a random string, default length is 16.
utils.randomString(32, '1234567890'); //18774480824014856763726145106142

// check if object has this property
utils.has({hello: 'world'}, 'hello'); //true

// empty function
utils.noop = function () {}
}
```

### Date utils

```js
// accessLogDate
utils.accessLogDate(); // '16/Apr/2013:16:40:09 +0800'

// logDate,
// 'YYYY-MM-DD HH:mm:ss.SSS' format date string
utils.logDate(); // '2013-04-17 14:43:02.674'
utils.YYYYMMDDHHmmssSSS(); // '2013-04-17 14:43:02.674'
utils.YYYYMMDDHHmmssSSS(','); // '2013-04-17 14:43:02,674'

// 'YYYY-MM-DD HH:mm:ss' format date string
utils.YYYYMMDDHHmmss(); // '2013-04-17 14:43:02'
utils.YYYYMMDDHHmmss(new Date(), {dateSep: '.'}); // '2013.04.17 14:43:02'

// 'YYYY-MM-DD' format date string
utils.YYYYMMDD(); // '2013-04-17'
utils.YYYYMMDD(''); // '20130417'
utils.YYYYMMDD(','); // '2013,04,17'

// datestruct
utils.datestruct(); // { YYYYMMDD: 20130416, H: 8 }

// Unix's timestamp
utils.timestamp(); // 1378153226

// Parse timestamp
// seconds
utils.timestamp(1385091596); // Fri Nov 22 2013 11:39:56 GMT+0800 (CST)
// millseconds
utils.timestamp(1385091596000); // Fri Nov 22 2013 11:39:56 GMT+0800 (CST)
```

### Number utils

```js
// Detect a number string can safe convert to Javascript Number.: `-9007199254740991 ~ 9007199254740991`
utils.isSafeNumberString('9007199254740991'); // true
utils.isSafeNumberString('9007199254740993'); // false

// Convert string to number safe:
utils.toSafeNumber('9007199254740991'); // 9007199254740991
utils.toSafeNumber('9007199254740993'); // '9007199254740993'

// Produces a random integer between the inclusive `lower` and exclusive `upper` bounds.
utils.random(100); // [0, 100)
utils.random(2, 1000); // [2, 1000)
utils.random(); // 0
```

### Timers

```js
utils.setImmediate(function () {
  console.log('hi');
});
```

### map

Create a `real` map in javascript.

use `Object.create(null)`

```js
const map = utils.map({a: 1});

// should.not.exist(map.constractor);
// should.not.exist(map.__proto__);
// should.not.exist(map.toString);
// should not exist any property

console.log(map); // {a: 1}
```

### String utils

```js
// split string by sep
utils.split('foo,bar,,,', ','); // ['foo', 'bar']

// replace string work with special chars which `String.prototype.replace` can't handle
utils.replace('<body> hi', '<body>', '$& body'); // '$& body hi'

// replace http header invalid characters
utils.replaceInvalidHttpHeaderChar('abc你好11'); // {invalid: true, val: 'abc  11'}
```

### Try

```js
const res = utils.try(function () {
  return JSON.parse(str);
});

// {error: undefined, value: {foo: 'bar'}}
// {error: Error, value: undefined}
```

### argumentsToArray

```js
function() {
  const arr = utility.argumentsToArray(arguments);
  console.log(arr.join(', '));
}
```

### JSON

```js
const obj = utils.strictJSONparse('"hello"');
// will throw when JSON string is not object

const pkg = utils.readJSONSync('package.json');
utils.writeJSONSync('package.json', pkg);
```

Or you can use async API

```js
async () => {
  const pkg = await utils.readJSON('package.json');
  await utils.writeJSON('package.json', pkg);
}
```

### Object.assign


```js
// assign object
utility.assign({}, { a: 1 });

// assign multiple object
utility.assign({}, [ { a: 1 }, { b: 1 } ]);
```

## benchmark

* [jsperf: access log date format](http://jsperf.com/access-log-date-format)
* [benchmark/date_format.js](https://github.com/fengmk2/utility/blob/master/benchmark/date_format.js)

```bash
$ node benchmark/date_format.js

moment().format("DD/MMM/YYYY:HH:mm:ss ZZ"): "16/Apr/2013:21:12:32 +0800"
utils.accessLogDate(): "16/Apr/2013:21:12:32 +0800"
fasterAccessDate(): "16/Apr/2013:21:12:32 +0800"
fasterAccessDate2(): "16/Apr/2013:21:12:32 +0800"
new Date().toString(): "Tue Apr 16 2013 21:12:32 GMT+0800 (CST)"
Date(): "Tue Apr 16 2013 21:12:32 GMT+0800 (CST)"
Date.now(): 1366117952162
------------------------
moment().format('DD/MMM/YYYY:HH:mm:ss ZZ') x 68,300 ops/sec ±5.05% (91 runs sampled)
utils.accessLogDate() x 1,341,341 ops/sec ±2.72% (90 runs sampled)
fasterAccessDate() x 357,833 ops/sec ±1.32% (98 runs sampled)
fasterAccessDate2() x 301,607 ops/sec ±5.03% (83 runs sampled)
new Date().toString() x 738,499 ops/sec ±3.54% (86 runs sampled)
Date() x 794,724 ops/sec ±2.77% (95 runs sampled)
Date.now() x 8,327,685 ops/sec ±1.85% (94 runs sampled)
Fastest is Date.now()
```

[benchmark/date_YYYYMMDD.js](https://github.com/fengmk2/utility/blob/master/benchmark/date_YYYYMMDD.js)

```bash
$ node benchmark/date_YYYYMMDD.js

parseInt(moment().format("YYYYMMDD"), 10): 20130416
utils.datestruct().YYYYMMDD: 20130416
new Date().toString(): "Tue Apr 16 2013 21:12:02 GMT+0800 (CST)"
------------------------
parseInt(moment().format('YYYYMMDD'), 10) x 129,604 ops/sec ±0.46% (101 runs sampled)
utils.datestruct().YYYYMMDD x 2,317,461 ops/sec ±1.38% (95 runs sampled)
new Date().toString() x 816,731 ops/sec ±3.46% (93 runs sampled)
Fastest is utils.datestruct().YYYYMMDD
```

## License

[MIT](LICENSE.txt)
