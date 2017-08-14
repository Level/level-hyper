level-hyper
===========

[![Greenkeeper badge](https://badges.greenkeeper.io/Level/level-hyper.svg)](https://greenkeeper.io/)

<img alt="LevelDB Logo" height="100" src="http://leveldb.org/img/logo.svg">

**Fast & simple storage - a Node.js-style HyperLevelDB wrapper**

[![NPM](https://nodei.co/npm/level-hyper.png)](https://nodei.co/npm/level-hyper/)

[![Build Status](https://secure.travis-ci.org/Level/level-hyper.png)](http://travis-ci.org/Level/level-hyper)
[![dependencies](https://david-dm.org/Level/level-hyper.svg)](https://david-dm.org/level/level-hyper)

This is a convenience package that bundles the current release of **[LevelUP](https://github.com/level/levelup)** and **[LevelDOWN-Hyper](https://github.com/level/leveldown-hyper)** and exposes LevelUP on its export.

Use this package to avoid having to explicitly install LevelDOWN-Hyper when you want to use LevelDOWN-Hyper with LevelUP.

<a name="usage"></a>
Usage
-----

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

The `.liveBackup()` method is accessible on the underlying `LevelDOWN-Hyper` object:

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

See **[LevelUP](https://github.com/level/levelup)** and **[LevelDOWN-Hyper](https://github.com/level/leveldown-hyper)** for more details.

<a name="contributing"></a>
Contributing
------------

**level-hyper** is an **OPEN Open Source Project**. This means that:

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is more like an open wiki than a standard guarded open source project.

See the [contribution guide](https://github.com/Level/community/blob/master/CONTRIBUTING.md) for more details.

<a name="licence"></a>
Licence &amp; Copyright
-------------------

Copyright (c) 2012-2016 **level-hyper** [contributors](https://github.com/level/community#contributors).

**level-hyper** is licensed under the MIT license. All rights not explicitly granted in the MIT license are reserved. See the included LICENSE.md file for more details.
