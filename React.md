# [Node.js]

### [babel.js]

**npm**

```sh
$ npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-react
$ npm install --save-dev babel-jest (optional)
```

**.babelrc**

```json
{
  "presets": [
    "react",
    ["env", {
      "targets": {
        "modules": false,
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
$ npm install --save-dev webpack html-webpack-plugin

$ npm install --save-dev webpack-dev-server (optional)
$ npm install --save-dev webpack-dev-middleware (optional)

$ npm install --save-dev babel-loader css-loader style-loader file-loader url-loader
$ npm install --save-dev scss-loader less-loader (optional) 

$ npm install --save-dev rimraf (optional)
```

**package.json**

* simple example with: webpack-dev-server
```json
{
    "scripts": {
      "clean": "rimraf dist",
      "build": "npm run clean && webpack",
      "build:prod": "NODE_ENV=production npm run clean && webpack -p",
      "serve": "webpack-dev-server",
      "deploy": "npm run build:prod && git subtree push --prefix dist origin gh-pages"
    }
}
```

* advance example with: webpack-dev-middleware
```json
{
    "scripts": {
      "clean": "rimraf dist",
      "build": "npm run clean && webpack",
      "build:prod": "NODE_ENV=production npm run clean && webpack -p",
      "serve": "webpack-dev-server",
      "deploy": "npm run build:prod && git subtree push --prefix dist origin gh-pages"
    }
}
```

**webpack.config.js**

```js
var webpack = require('webpack');
var path = require('path');
var fs = require('fs');

var VENDOR_LIBS = [
  'react', 'react-dom'
];

module.exports = {
  entry: {
    bundle: './src/index.js',
    vendor: VENDOR_LIBS
  },
  output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name].[chunckhash].js'
  },
  resolve: {
    extensions: ['*', '.js', '.jsx', '.json']
  },
  devtool: 'sourcemap',
  module: {
    rules: [
      {
        use: 'babel-loader',
        test: '/\.js$/',
        exclude: '/node_modules/'
      }
    ]
  },
  plugins: [
    new webpack.optimize.CommonsChunckPlugin({
      name: ['vendor', 'manifest']
    }),
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV)
    })
  ]
}
```

### [express.js]

**npm**

```sh
$ npm install --save express
```

**server.js**

```js
const path = require('path');
const express = require('express');

const app = express();

// Server routes
app.get('/api', (req, res) => res.send({version: 'v0'}));

if (process.env.NODE_ENV !== 'production') {
  const webpackMiddleware = require('webpack-dev-middleware');
  const webpack = require('webpack');
  const webpackConfig = require('./webpack.config.js')
  
  app.use(webpackMiddleware(webpack(webpackConfig)));
} else {
  app.use(express.static('dist'));
  app.get('*', (req, res) => {
    res.sendFile(path.join(__dirname, 'dist/index.html'));
  })
}

app.listen(process.env.PORT || 3050, () => console.log('Listening'));
```

### [heroku]

**Procfile**

```text
web: node server.js
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