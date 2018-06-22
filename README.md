# level-hyper

> Fast & simple storage - a Node.js-style HyperLevelDB wrapper

[![level badge][level-badge]](https://github.com/level/awesome)
[![npm](https://img.shields.io/npm/v/level-hyper.svg)](https://www.npmjs.com/package/level-hyper)
![Node version](https://img.shields.io/node/v/level-hyper.svg)
[![Build Status](https://img.shields.io/travis/Level/level-hyper.png)](https://travis-ci.org/Level/level-hyper)
[![dependencies](https://david-dm.org/Level/level-hyper.svg)](https://david-dm.org/level/level-hyper)
[![npm](https://img.shields.io/npm/dm/level-hyper.svg)](https://www.npmjs.com/package/level-hyper)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

This is a convenience package that bundles the current release of **[levelup](https://github.com/level/levelup)** and **[leveldown-hyper](https://github.com/level/leveldown-hyper)** and exposes `levelup` on its export.

Use this package to avoid having to explicitly install `leveldown-hyper` when you want to use `leveldown-hyper` with `levelup`.

## Usage

Basic usage for putting and getting data:

```js
var level = require('level-hyper')

// 1) Create our database, supply location and options.
//    This will create or open the underlying LevelDB store.
var db = level('./mydb')

// 2) put a key & value
db.put('name', 'Level', function (err) {
  if (err) return console.log('Ooops!', err) // some kind of I/O error

  // 3) fetch by key
  db.get('name', function (err, value) {
    if (err) return console.log('Ooops!', err) // likely the key was not found

    // ta da!
    console.log('name=' + value)
  })
})
```

The `.liveBackup()` method is accessible on the underlying `leveldown-hyper` object:

```js
var level = require('level-hyper')
var db = level('./mydb')
db.on('ready', function () {
  var name = String(Date.now())
  db.db.liveBackup(name, function (err) {
    if (!err) console.log('backup to %s was successful', name)
  })
})
```

See **[levelup](https://github.com/level/levelup)** and **[leveldown-hyper](https://github.com/level/leveldown-hyper)** for more details.

## Contributing

`level-hyper` is an **OPEN Open Source Project**. This means that:

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is more like an open wiki than a standard guarded open source project.

See the [contribution guide](https://github.com/Level/community/blob/master/CONTRIBUTING.md) for more details.

## License

[MIT](./LICENSE.md) © 2012-present `level-hyper` [Contributors](./CONTRIBUTORS.md).

[level-badge]: http://leveldb.org/img/badge.svg
