# Prerequisites

> MacOS Sierra 10.12.6

> npm version

```
{
  'typescript-eslint': '1.0.0',
  npm: '5.0.3',
  ares: '1.10.1-DEV',
  cldr: '31.0.1',
  http_parser: '2.7.0',
  icu: '59.1',
  modules: '57',
  node: '8.1.2',
  openssl: '1.0.2l',
  tz: '2017b',
  unicode: '9.0',
  uv: '1.12.0',
  v8: '5.8.283.41',
  zlib: '1.2.11'
}
  ```

# Description

Typescript parser for eslint causing error in [`eslint-plugin-react`](https://github.com/yannickcr/eslint-plugin-react).

Seems related to `typescript-eslint-parser` issue [#70](https://github.com/eslint/typescript-eslint-parser/issues/70).

To reproduce:

> npm run lint_breaks

```
Cannot read property 'type' of null
TypeError: Cannot read property 'type' of null
    at Linter.JSXOpeningElement (/typescript-eslint/node_modules/eslint-plugin-react/lib/rules/jsx-indent.js:229:32)
    at emitOne (events.js:120:20)
    at Linter.emit (events.js:210:7)
    at NodeEventGenerator.applySelector (/typescript-eslint/node_modules/eslint/lib/util/node-event-generator.js:265:26)
    at NodeEventGenerator.applySelectors (/typescript-eslint/node_modules/eslint/lib/util/node-event-generator.js:294:22)
    at NodeEventGenerator.enterNode (/typescript-eslint/node_modules/eslint/lib/util/node-event-generator.js:308:14)
    at CodePathAnalyzer.enterNode (/typescript-eslint/node_modules/eslint/lib/code-path-analysis/code-path-analyzer.js:602:23)
    at Traverser.enter (/typescript-eslint/node_modules/eslint/lib/linter.js:925:36)
    at Traverser.__execute (/typescript-eslint/node_modules/estraverse/estraverse.js:397:31)
    at Traverser.traverse (/typescript-eslint/node_modules/estraverse/estraverse.js:501:28)
```

> npm run lint_works

Lints file normally.

The diff out of `test.works.tsx` and `test.breaks.tsx`:

```
@@ -2,8 +2,7 @@ import React from 'react'

 export default class Test extends React.PureComponent {
   render () {
-    return <div>
-      <div>
+    return <div><div>
         Breaks
       </div>
     </div>
```
