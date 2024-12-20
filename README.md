# level-hyper

**Discontinued.**

---

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

## License

[MIT](LICENSE.md) © 2012-present [Contributors](CONTRIBUTORS.md).
