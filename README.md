# level-hyper

> Fast & simple storage - a Node.js-style HyperLevelDB wrapper

[![level badge][level-badge]](https://github.com/Level/awesome)
[![npm](https://img.shields.io/npm/v/level-hyper.svg?label=&logo=npm)](https://www.npmjs.com/package/level-hyper)
[![Node version](https://img.shields.io/node/v/level-hyper.svg)](https://www.npmjs.com/package/level-hyper)
[![Travis](https://img.shields.io/travis/Level/level-hyper.svg?logo=travis&label=)](https://travis-ci.org/Level/level-hyper)
[![npm](https://img.shields.io/npm/dm/level-hyper.svg?label=dl)](https://www.npmjs.com/package/level-hyper)
[![Coverage Status](https://coveralls.io/repos/github/Level/level-hyper/badge.svg)](https://coveralls.io/github/Level/level-hyper)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![Backers on Open Collective](https://opencollective.com/level/backers/badge.svg?color=orange)](#backers)
[![Sponsors on Open Collective](https://opencollective.com/level/sponsors/badge.svg?color=orange)](#sponsors)

This is a convenience package that bundles the current release of **[levelup](https://github.com/Level/levelup)** and **[leveldown-hyper](https://github.com/Level/leveldown-hyper)** and exposes `levelup` on its export.

Use this package to avoid having to explicitly install `leveldown-hyper` when you want to use `leveldown-hyper` with `levelup`.

**If you are upgrading:** please see [`UPGRADING.md`](UPGRADING.md).

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

See **[levelup](https://github.com/Level/levelup)** and **[leveldown-hyper](https://github.com/Level/leveldown-hyper)** for more details.

## Contributing

[`Level/level-hyper`](https://github.com/Level/level-hyper) is an **OPEN Open Source Project**. This means that:

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is more like an open wiki than a standard guarded open source project.

See the [Contribution Guide](https://github.com/Level/community/blob/master/CONTRIBUTING.md) for more details.

## Donate

To sustain [`Level`](https://github.com/Level) and its activities, become a backer or sponsor on [Open Collective](https://opencollective.com/level). Your logo or avatar will be displayed on our 28+ [GitHub repositories](https://github.com/Level) and [npm](https://www.npmjs.com/) packages. 💖

### Backers

[![Open Collective backers](https://opencollective.com/level/backers.svg?width=890)](https://opencollective.com/level)

### Sponsors

[![Open Collective sponsors](https://opencollective.com/level/sponsors.svg?width=890)](https://opencollective.com/level)

## License

[MIT](LICENSE.md) © 2012-present [Contributors](CONTRIBUTORS.md).

[level-badge]: https://leveljs.org/img/badge.svg
