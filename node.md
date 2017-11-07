# [Node.js]

### [babel.js]

**npm**

```sh
$ npm install --save babel-polyfill

$ npm install --save-dev babel-cli babel-preset-env
$ npm install --save-dev babel-jest (optional)
```

**.babelrc**

```json
{
  "presets": [
    ["env", {
      "targets": {
        "node": "current",
        "browsers": ["> 1%", "last 2 versions"]
      }
    }]
  ]
}
```

**app.js**

```js
import "babel-polyfill";
```

### [webpack]

**npm**

```sh
$ npm install --save-dev webpack source-map-support
```

**package.json**

```json
{
    "scripts": {
      "build": "webpack --watch"
    }
}
```

**webpack.config.js**

```js
var webpack = require('webpack');
var path = require('path');
var fs = require('fs');

var nodeModules = {};
fs.readdirSync('node_modules')
  .filter(function(x) {
    return ['.bin'].indexOf(x) === -1;
  })
  .forEach(function(mod) {
    nodeModules[mod] = 'commonjs ' + mod;
  });

module.exports = {
  entry: './src/main.js',
  target: 'node',
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'backend.js'
  },
  devtool: 'sourcemap',
  externals: nodeModules,
  plugins: [
    new webpack.IgnorePlugin(/\.(css|scss|less)$/),
    new webpack.BannerPlugin(
      'require("source-map-support").install();',
      {raw: true, entryOnly: false}
    )
  ]
}
```

### [mongodb]
### [express.js]

**npm**

```sh
$ npm install --save express
```

### [eslint]

### [editorconfig]

**.editorconfig**

```text
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false
```

### [mocha]
### [jest]

[//]: #
  [Node.js]: <https://nodejs.org/>
  [babel.js]: <https://babeljs.io/>
  [webpack]: <https://webpack.js.org/>
  [mongodb]: <https://www.mongodb.com/>
  [express.js]: <https://expressjs.com/>
  [eslint]: <https://eslint.org/>
  [editorconfig]: <editorconfig.org>
  [mocha]: <https://mochajs.org/>
  [jest]: <https://facebook.github.io/jest/>