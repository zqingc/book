



执行的是package.json 里面的东西

`npm run dev`

```js
"scripts": {
"dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",

"start": "npm run dev",

"unit": "jest --config test/unit/jest.conf.js --coverage",

"e2e": "node test/e2e/runner.js",

"test": "npm run unit && npm run e2e",

"lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",

"build": "node build/build.js"
 }
```
