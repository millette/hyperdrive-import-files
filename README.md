
# hyperdrive-import-files

Import some files and folders into a [hyperdrive](https://github.com/mafintosh/hyperdrive), and optionally keep watching for changes.

[![Build Status](https://travis-ci.org/juliangruber/hyperdrive-import-files.svg?branch=master)](https://travis-ci.org/juliangruber/hyperdrive-import-files)

## Example

```js
const hyperdrive = require('hyperdrive')
const memdb = require('memdb')
const hyperImport = require('hyperdrive-import-files')

const drive = hyperdrive(memdb())
const archive = drive.createArchive()

hyperImport(archive, [
  'a/directory/',
  'some/file.txt'
], err => {
  // ...
})
```

## Installation

```bash
$ npm install hyperdrive-import-files
```

## API

### hyperImport(archive, files, [, options], cb)

Recursively import `files` into `archive` and call `cb` with the potential error. The import happens sequentually. Returns a `status` object.

To enable watching, set `live: true`, like this:

```js
const status = hyperImport(archive, files, { live: true }, err => {
  console.log('initial import done')  
})
status.on('error', err => {
  // ...  
})
// when you want to quit:
status.close()
```

### status

Events:

- `error` (`err`)
- `file imported` (`path`)

Properties:

- `fileCount`: The count of currently known files
- `totalSize`: Total file size in bytes

## License

MIT
