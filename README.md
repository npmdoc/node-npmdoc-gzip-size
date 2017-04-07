# api documentation for  [gzip-size (v3.0.0)](https://github.com/sindresorhus/gzip-size)  [![npm package](https://img.shields.io/npm/v/npmdoc-gzip-size.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gzip-size) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gzip-size.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gzip-size)
#### Get the gzipped size of a string or buffer

[![NPM](https://nodei.co/npm/gzip-size.png?downloads=true)](https://www.npmjs.com/package/gzip-size)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gzip-size/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gzip-size_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gzip-size/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gzip-size/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gzip-size/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sindre Sorhus",
        "email": "sindresorhus@gmail.com",
        "url": "sindresorhus.com"
    },
    "bugs": {
        "url": "https://github.com/sindresorhus/gzip-size/issues"
    },
    "dependencies": {
        "duplexer": "^0.1.1"
    },
    "description": "Get the gzipped size of a string or buffer",
    "devDependencies": {
        "tap": "^1.3.2",
        "xo": "*"
    },
    "directories": {},
    "dist": {
        "shasum": "546188e9bdc337f673772f81660464b389dce520",
        "tarball": "https://registry.npmjs.org/gzip-size/-/gzip-size-3.0.0.tgz"
    },
    "engines": {
        "node": ">=0.12.0"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "55cd41dd1ff020282b2e9fe47620e71838d29646",
    "homepage": "https://github.com/sindresorhus/gzip-size",
    "keywords": [
        "app",
        "tool",
        "zlib",
        "gzip",
        "compressed",
        "size",
        "string",
        "buffer"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "sindresorhus",
            "email": "sindresorhus@gmail.com"
        }
    ],
    "name": "gzip-size",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/sindresorhus/gzip-size.git"
    },
    "scripts": {
        "test": "xo && tap test.js"
    },
    "version": "3.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gzip-size](#apidoc.module.gzip-size)
1.  [function <span class="apidocSignatureSpan">gzip-size.</span>stream ()](#apidoc.element.gzip-size.stream)
1.  [function <span class="apidocSignatureSpan">gzip-size.</span>sync (str)](#apidoc.element.gzip-size.sync)



# <a name="apidoc.module.gzip-size"></a>[module gzip-size](#apidoc.module.gzip-size)

#### <a name="apidoc.element.gzip-size.stream"></a>[function <span class="apidocSignatureSpan">gzip-size.</span>stream ()](#apidoc.element.gzip-size.stream)
- description and source-code
```javascript
stream = function () {
	var input = new stream.PassThrough();
	var output = new stream.PassThrough();
	var wrapper = duplexer(input, output);

	var gzipSize = 0;
	var gzip = zlib.createGzip(opts)
		.on('data', function (buf) {
			gzipSize += buf.length;
		})
		.on('error', function () {
			wrapper.gzipSize = 0;
		})
		.on('end', function () {
			wrapper.gzipSize = gzipSize;
			wrapper.emit('gzip-size', gzipSize);
			output.end();
		});

	input.pipe(gzip);
	input.pipe(output, {end: false});

	return wrapper;
}
```
- example usage
```shell
...

Type: 'string', 'buffer'

#### callback(error, size)

Type: 'function'

### gzipSize.stream()

Returns a passthrough stream. The stream emits a 'gzip-size' event and has a 'gzipSize' property.


## Related

- [gzip-size-cli](https://github.com/sindresorhus/gzip-size-cli) - CLI for this module
...
```

#### <a name="apidoc.element.gzip-size.sync"></a>[function <span class="apidocSignatureSpan">gzip-size.</span>sync (str)](#apidoc.element.gzip-size.sync)
- description and source-code
```javascript
sync = function (str) {
	return zlib.gzipSync(str, opts).length;
}
```
- example usage
```shell
...
'''js
var gzipSize = require('gzip-size');
var string = 'Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis
 natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.';

console.log(string.length);
//=> 191

console.log(gzipSize.sync(string));
//=> 78
'''


## API

### gzipSize(input, callback)
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
