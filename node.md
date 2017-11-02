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

[//]: #
   [Node.js]: <https://nodejs.org/>
   [babel.js]: <https://babeljs.io/>