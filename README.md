# YAML <a href="https://www.npmjs.com/package/yaml"><img align="right" src="https://badge.fury.io/js/yaml.svg" title="npm package" /></a>

`yaml` is a definitive library for [YAML](http://yaml.org/), the human friendly data serialization standard.
This library:

- Supports both YAML 1.1 and YAML 1.2 and all common data schemas,
- Passes all of the [yaml-test-suite](https://github.com/yaml/yaml-test-suite) tests,
- Can accept any string as input without throwing, parsing as much YAML out of it as it can, and
- Supports parsing, modifying, and writing YAML comments and blank lines.

The library is released under the ISC open source license, and the code is [available on GitHub](https://github.com/eemeli/yaml/).
It has no external dependencies and runs on Node.js as well as modern browsers.

For the purposes of versioning, any changes that break any of the documented endpoints or APIs will be considered semver-major breaking changes.
Undocumented library internals may change between minor versions, and previous APIs may be deprecated (but not removed).

For more information, see the project's documentation site: [**eemeli.org/yaml**](https://eemeli.org/yaml/)

To install:

```sh
npm install yaml
```

**Note:** These docs are for `yaml@2`. For v1, see the [v1.10.0 tag](https://github.com/eemeli/yaml/tree/v1.10.0) for the source and [eemeli.org/yaml/v1](https://eemeli.org/yaml/v1/) for the documentation.

## API Overview

The API provided by `yaml` has three layers, depending on how deep you need to go: [Parse & Stringify](https://eemeli.org/yaml/#parse-amp-stringify), [Documents](https://eemeli.org/yaml/#documents), and the underlying [Lexer/Parser/Composer](https://eemeli.org/yaml/#parsing-yaml).
The first has the simplest API and "just works", the second gets you all the bells and whistles supported by the library along with a decent [AST](https://eemeli.org/yaml/#content-nodes), and the third lets you get progressively closer to YAML source, if that's your thing.

```js
import { parse, stringify } from 'yaml'
// or
import YAML from 'yaml'
// or
const YAML = require('yaml')
```

### Parse & Stringify

- [`parse(str, reviver?, options?): value`](https://eemeli.org/yaml/#yaml-parse)
- [`stringify(value, replacer?, options?): string`](https://eemeli.org/yaml/#yaml-stringify)

### Documents

- [`Document`](https://eemeli.org/yaml/#documents)
  - [`constructor(value, replacer?, options?)`](https://eemeli.org/yaml/#creating-documents)
  - [`#anchors`](https://eemeli.org/yaml/#working-with-anchors)
  - [`#contents`](https://eemeli.org/yaml/#content-nodes)
  - [`#directives`](https://eemeli.org/yaml/#stream-directives)
  - [`#errors`](https://eemeli.org/yaml/#errors)
  - [`#warnings`](https://eemeli.org/yaml/#errors)
- [`isDocument(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`parseAllDocuments(str, options?): Document[]`](https://eemeli.org/yaml/#parsing-documents)
- [`parseDocument(str, options?): Document`](https://eemeli.org/yaml/#parsing-documents)

### Content Nodes

- [`isAlias(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isCollection(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isMap(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isNode(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isPair(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isScalar(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`isSeq(foo): boolean`](https://eemeli.org/yaml/#identifying-nodes)
- [`new Scalar(value)`](https://eemeli.org/yaml/#scalar-values)
- [`new YAMLMap()`](https://eemeli.org/yaml/#collections)
- [`new YAMLSeq()`](https://eemeli.org/yaml/#collections)
- [`doc.createAlias(node, name?): Alias`](https://eemeli.org/yaml/#working-with-anchors)
- [`doc.createNode(value, options?): Node`](https://eemeli.org/yaml/#creating-nodes)
- [`doc.createPair(key, value): Pair`](https://eemeli.org/yaml/#creating-nodes)
- [`visit(node, visitor)`](https://eemeli.org/yaml/#modifying-nodes)

### Parsing YAML

- [`new Lexer().lex(src)`](https://eemeli.org/yaml/#lexer)
- [`new Parser(onNewLine?).parse(src)`](https://eemeli.org/yaml/#parser)
- [`new Composer(options?).compose(tokens)`](https://eemeli.org/yaml/#composer)

## YAML.parse

```yaml
# file.yml
YAML:
  - A human-readable data serialization language
  - https://en.wikipedia.org/wiki/YAML
yaml:
  - A complete JavaScript implementation
  - https://www.npmjs.com/package/yaml
```

```js
import fs from 'fs'
import YAML from 'yaml'

YAML.parse('3.14159')
// 3.14159

YAML.parse('[ true, false, maybe, null ]\n')
// [ true, false, 'maybe', null ]

const file = fs.readFileSync('./file.yml', 'utf8')
YAML.parse(file)
// { YAML:
//   [ 'A human-readable data serialization language',
//     'https://en.wikipedia.org/wiki/YAML' ],
//   yaml:
//   [ 'A complete JavaScript implementation',
//     'https://www.npmjs.com/package/yaml' ] }
```

## YAML.stringify

```js
import YAML from 'yaml'

YAML.stringify(3.14159)
// '3.14159\n'

YAML.stringify([true, false, 'maybe', null])
// `- true
// - false
// - maybe
// - null
// `

YAML.stringify({ number: 3, plain: 'string', block: 'two\nlines\n' })
// `number: 3
// plain: string
// block: |
//   two
//   lines
// `
```

---

Browser testing provided by:

<a href="https://www.browserstack.com/open-source">
<img width=200 src="https://eemeli.org/yaml/images/browserstack.svg" />
</a>
