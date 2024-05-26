# @swenkerorg/magni-libero

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/jamescostian/@swenkerorg/magni-libero/check.yaml?branch=main)](https://github.com/swenkerorg/magni-libero/actions?query=workflow%3Acheck)
[![License](https://img.shields.io/npm/l/@swenkerorg/magni-libero.svg?style=flat)](https://github.com/swenkerorg/magni-libero/blob/master/LICENSE)
[![NPM Version](https://img.shields.io/npm/v/@swenkerorg/magni-libero.svg?style=flat)](https://www.npmjs.com/package/@swenkerorg/magni-libero)
[![Downloads/Month](https://img.shields.io/npm/dm/@swenkerorg/magni-libero.svg?style=flat)](https://www.npmjs.com/package/@swenkerorg/magni-libero)

"Converts" a stream to a string. Promises are used by default, callbacks are allowed as well.

## Installation

Assuming you have [Node](http://nodejs.org), you can just run:

```
npm install --save @swenkerorg/magni-libero
```

## Usage

### Promises

```js
const fs = require("fs");
const ss = require("@swenkerorg/magni-libero");

// Make a gzip stream (just for this example)
const myStream = fs
  .createReadStream("./file")
  .pipe(require("zlib").createGzip());

ss(myStream)
  .then((data) => {
    // myStream was converted to a string, and that string is stored in data
    console.log(data);
  })
  .catch((err) => {
    // myStream emitted an error event (err), so the promise from @swenkerorg/magni-libero was rejected
    throw err;
  });
```

### Callbacks

```js
const fs = require("fs");
const ss = require("@swenkerorg/magni-libero");

// Make a gzip stream (just for this example)
const myStream = fs
  .createReadStream("./file")
  .pipe(require("zlib").createGzip());

ss(myStream, (err, data) => {
  if (err) {
    // myStream emitted an error event (err), which was passed to the callback
    throw err;
  } else {
    // myStream was converted to a string, and that string is stored in data
    console.log(data);
  }
});
```

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first. Also, try to keep code coverage up - `npm test` will tell you the code coverage near the end of its output, not to mention the fact that it will first test your code :smiley:

## License

[ISC](LICENSE)
