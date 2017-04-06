# api documentation for  [byline (v5.0.0)](https://github.com/jahewson/node-byline)  [![npm package](https://img.shields.io/npm/v/npmdoc-byline.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-byline) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-byline.svg)](https://travis-ci.org/npmdoc/node-npmdoc-byline)
#### simple line-by-line stream reader

[![NPM](https://nodei.co/npm/byline.png?downloads=true)](https://www.npmjs.com/package/byline)

[![apidoc](https://npmdoc.github.io/node-npmdoc-byline/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-byline_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-byline/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-byline/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-byline/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "John Hewson"
    },
    "bugs": {
        "url": "https://github.com/jahewson/node-byline/issues"
    },
    "dependencies": {},
    "description": "simple line-by-line stream reader",
    "devDependencies": {
        "mocha": "~2.1.0",
        "request": "~2.27.0"
    },
    "directories": {},
    "dist": {
        "shasum": "741c5216468eadc457b03410118ad77de8c1ddb1",
        "tarball": "https://registry.npmjs.org/byline/-/byline-5.0.0.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "files": [
        "lib"
    ],
    "gitHead": "3335926be164882b8d12ea9f4ac9f44c083bc3fc",
    "homepage": "https://github.com/jahewson/node-byline",
    "license": "MIT",
    "main": "./lib/byline.js",
    "maintainers": [
        {
            "name": "jahewson",
            "email": "johnahewson@yahoo.co.uk"
        }
    ],
    "name": "byline",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/jahewson/node-byline.git"
    },
    "scripts": {
        "test": "mocha -R spec --timeout 60000"
    },
    "version": "5.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module byline](#apidoc.module.byline)
1.  [function <span class="apidocSignatureSpan">byline.</span>LineStream (options)](#apidoc.element.byline.LineStream)
1.  [function <span class="apidocSignatureSpan">byline.</span>createLineStream (readStream)](#apidoc.element.byline.createLineStream)
1.  [function <span class="apidocSignatureSpan">byline.</span>createStream (readStream, options)](#apidoc.element.byline.createStream)
1.  object <span class="apidocSignatureSpan">byline.</span>LineStream.prototype

#### [module byline.LineStream](#apidoc.module.byline.LineStream)
1.  [function <span class="apidocSignatureSpan">byline.</span>LineStream (options)](#apidoc.element.byline.LineStream.LineStream)
1.  [function <span class="apidocSignatureSpan">byline.LineStream.</span>super_ (options)](#apidoc.element.byline.LineStream.super_)

#### [module byline.LineStream.prototype](#apidoc.module.byline.LineStream.prototype)
1.  [function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_flush (done)](#apidoc.element.byline.LineStream.prototype._flush)
1.  [function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_pushBuffer (encoding, keep, done)](#apidoc.element.byline.LineStream.prototype._pushBuffer)
1.  [function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_reencode (line, chunkEncoding)](#apidoc.element.byline.LineStream.prototype._reencode)
1.  [function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_transform (chunk, encoding, done)](#apidoc.element.byline.LineStream.prototype._transform)



# <a name="apidoc.module.byline"></a>[module byline](#apidoc.module.byline)

#### <a name="apidoc.element.byline.LineStream"></a>[function <span class="apidocSignatureSpan">byline.</span>LineStream (options)](#apidoc.element.byline.LineStream)
- description and source-code
```javascript
function LineStream(options) {
  stream.Transform.call(this, options);
  options = options || {};

  // use objectMode to stop the output from being buffered
  // which re-concatanates the lines, just without newlines.
  this._readableState.objectMode = true;
  this._lineBuffer = [];
  this._keepEmptyLines = options.keepEmptyLines || false;
  this._lastChunkEndedWithCR = false;

  // take the source's encoding if we don't have one
  var self = this;
  this.on('pipe', function(src) {
    if (!self.encoding) {
      // but we can't do this for old-style streams
      if (src instanceof stream.Readable) {
        self.encoding = src._readableState.encoding;
      }
    }
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.createLineStream"></a>[function <span class="apidocSignatureSpan">byline.</span>createLineStream (readStream)](#apidoc.element.byline.createLineStream)
- description and source-code
```javascript
createLineStream = function (readStream) {
  console.log('WARNING: byline#createLineStream is deprecated and will be removed soon');
  return createLineStream(readStream);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.createStream"></a>[function <span class="apidocSignatureSpan">byline.</span>createStream (readStream, options)](#apidoc.element.byline.createStream)
- description and source-code
```javascript
createStream = function (readStream, options) {
  if (readStream) {
    return createLineStream(readStream, options);
  } else {
    return new LineStream(options);
  }
}
```
- example usage
```shell
...
You just need to add one line to wrap your readable 'Stream' with a 'LineStream'.

'''javascript
var fs = require('fs'),	
    byline = require('byline');

var stream = fs.createReadStream('sample.txt');
stream = byline.createStream(stream);

stream.on('data', function(line) {
  console.log(line);
});
'''

# Piping
...
```



# <a name="apidoc.module.byline.LineStream"></a>[module byline.LineStream](#apidoc.module.byline.LineStream)

#### <a name="apidoc.element.byline.LineStream.LineStream"></a>[function <span class="apidocSignatureSpan">byline.</span>LineStream (options)](#apidoc.element.byline.LineStream.LineStream)
- description and source-code
```javascript
function LineStream(options) {
  stream.Transform.call(this, options);
  options = options || {};

  // use objectMode to stop the output from being buffered
  // which re-concatanates the lines, just without newlines.
  this._readableState.objectMode = true;
  this._lineBuffer = [];
  this._keepEmptyLines = options.keepEmptyLines || false;
  this._lastChunkEndedWithCR = false;

  // take the source's encoding if we don't have one
  var self = this;
  this.on('pipe', function(src) {
    if (!self.encoding) {
      // but we can't do this for old-style streams
      if (src instanceof stream.Readable) {
        self.encoding = src._readableState.encoding;
      }
    }
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.LineStream.super_"></a>[function <span class="apidocSignatureSpan">byline.LineStream.</span>super_ (options)](#apidoc.element.byline.LineStream.super_)
- description and source-code
```javascript
function Transform(options) {
  if (!(this instanceof Transform))
    return new Transform(options);

  Duplex.call(this, options);

  this._transformState = new TransformState(this);

  var stream = this;

  // start out asking for a readable event once data is transformed.
  this._readableState.needReadable = true;

  // we have implemented the _read method, and done the other things
  // that Readable wants before the first _read call, so unset the
  // sync guard flag.
  this._readableState.sync = false;

  if (options) {
    if (typeof options.transform === 'function')
      this._transform = options.transform;

    if (typeof options.flush === 'function')
      this._flush = options.flush;
  }

  // When the writable side finishes, then flush out anything remaining.
  this.once('prefinish', function() {
    if (typeof this._flush === 'function')
      this._flush(function(er) {
        done(stream, er);
      });
    else
      done(stream);
  });
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.byline.LineStream.prototype"></a>[module byline.LineStream.prototype](#apidoc.module.byline.LineStream.prototype)

#### <a name="apidoc.element.byline.LineStream.prototype._flush"></a>[function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_flush (done)](#apidoc.element.byline.LineStream.prototype._flush)
- description and source-code
```javascript
_flush = function (done) {
  this._pushBuffer(this._chunkEncoding, 0, done);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.LineStream.prototype._pushBuffer"></a>[function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_pushBuffer (encoding, keep, done)](#apidoc.element.byline.LineStream.prototype._pushBuffer)
- description and source-code
```javascript
_pushBuffer = function (encoding, keep, done) {
  // always buffer the last (possibly partial) line
  while (this._lineBuffer.length > keep) {
    var line = this._lineBuffer.shift();
    // skip empty lines
    if (this._keepEmptyLines || line.length > 0 ) {
      if (!this.push(this._reencode(line, encoding))) {
        // when the high-water mark is reached, defer pushes until the next tick
        var self = this;
        timers.setImmediate(function() {
          self._pushBuffer(encoding, keep, done);
        });
        return;
      }
    }
  }
  done();
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.LineStream.prototype._reencode"></a>[function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_reencode (line, chunkEncoding)](#apidoc.element.byline.LineStream.prototype._reencode)
- description and source-code
```javascript
_reencode = function (line, chunkEncoding) {
  if (this.encoding && this.encoding != chunkEncoding) {
    return new Buffer(line, chunkEncoding).toString(this.encoding);
  }
  else if (this.encoding) {
    // this should be the most common case, i.e. we're using an encoded source stream
    return line;
  }
  else {
    return new Buffer(line, chunkEncoding);
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.byline.LineStream.prototype._transform"></a>[function <span class="apidocSignatureSpan">byline.LineStream.prototype.</span>_transform (chunk, encoding, done)](#apidoc.element.byline.LineStream.prototype._transform)
- description and source-code
```javascript
_transform = function (chunk, encoding, done) {
  // decode binary chunks as UTF-8
  encoding = encoding || 'utf8';

  if (Buffer.isBuffer(chunk)) {
    if (encoding == 'buffer') {
      chunk = chunk.toString(); // utf8
      encoding = 'utf8';
    }
    else {
     chunk = chunk.toString(encoding);
    }
  }
  this._chunkEncoding = encoding;

  // see: http://www.unicode.org/reports/tr18/#Line_Boundaries
  var lines = chunk.split(/\r\n|[\n\v\f\r\x85\u2028\u2029]/g);

  // don't split CRLF which spans chunks
  if (this._lastChunkEndedWithCR && chunk[0] == '\n') {
    lines.shift();
  }

  if (this._lineBuffer.length > 0) {
    this._lineBuffer[this._lineBuffer.length - 1] += lines[0];
    lines.shift();
  }

  this._lastChunkEndedWithCR = chunk[chunk.length - 1] == '\r';
  this._lineBuffer = this._lineBuffer.concat(lines);
  this._pushBuffer(encoding, 1, done);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
