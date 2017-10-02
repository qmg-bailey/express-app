``
npm init -y
``

``
npm install --save express
``



Then your **package.json** should look like this:
```
{
  "name": "express-vanilla",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.1"
  }
}

```


Don't forget to create a **.gitignore** file to hide your node_modules from git:
```
node_modules
```

Create an **index.js** file at the root and do a quick configuration of your express app:

```
const express = require('express');
const app = express();

app.get('/', function(req, res) {
  res.send('Hello world!');
});

app.listen(3000, function() {
  console.log('app listening on port 3000');
});

```

To let your new app accept javascript written the es6 way, you need to add babel to compile the raw code back into es5:

``
npm install --save-dev babel-cli babel-preset-env
``

Then you need to configure your babel setup in a new **.babelrc** file:

```
{
  "presets": ["env"]
}
```

Plus add two scripts to your **package.json** - a build script and a start script. The build script takes all of the files in your root and outputs a compiled version in the dist folder, ignoring the folders and files you'e specified. The start script then builds and runs the code.

```
"build": "babel ./ --out-dir dist/ --ignore ./node_modules,./.babelrc,./package.json,./npm-debug.log --copy-files",
"start": "npm run build && node dist/index.js"
```
