# @imarkjs/remark-code

## Introduction

an extension for `unified` to enable code syntax, support that parse `AST` from `markdown` and compile `AST` into `markdown`.

## Features

1. Compatible with standard code syntax.
    <br/>
    \`\`\`lang metadata <br/>
    code <br/>
    \`\`\`<br/>

2. Expending a new feature `props`.
    <br/>
    \`\`\`lang metadata <br/>
    code <br/>
    \`\`\`{{props}} <br/>

## Using

### Install

```bash
npm i unified remark-parse remark-stringify @imarkjs/remark-code -S
```

### Example

```javascript

import {unified} from 'unified'
import remarkParse from 'remark-parse'
import remarkStringify from 'remark-stringify'
import remarkCode from '@imarkjs/remark-code'

const str = `
# Example
\`\`\`lang meta
let s = 'hi'
console.log(s)
\`\`\`{{properties}}
`

const processor1 = unified()
    .use(remarkParse)
    .use(remarkCode)
const ast = processor1.parse(str)
console.log('ast ->', ast)

const processor2 = unified()
    .use(remarkParse)
    .use(remarkCode)
    .use(remarkStringify)
const md = processor2.stringify(ast)
console.log('markdown ->', md)

```

run it, you will get result as following:

```bash
ast -> {
  type: 'root',
  children: [
    {
      type: 'heading',
      depth: 1,
      children: [Array],
      position: [Object]
    },
    {
      type: 'code',
      lang: 'lang',
      meta: 'meta',
      props: 'properties',
      value: "\nlet s = 'hi'\nconsole.log(s)\n",
      position: [Object]
    }
  ],
  position: {
    start: { line: 1, column: 1, offset: 0 },
    end: { line: 6, column: 1, offset: 69 }
  }
}

# note: use ''' to beautify \`\`\`. 

markdown -> # Example

'''lang meta
let s = 'hi'
console.log(s)
'''{{properties}}
```

## How does it works ?

![How does it works?](./readme.png)