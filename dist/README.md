# An 'Easy' Node, Express, Postgres, Knex, React App

### 1. Get your Node/Express app up and running
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

## 2. Enter the 21st Century and code with ES6

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

Add rimraf as a dependancy so that the **dist** folder can be wiped every time babel recompiles:

``
npm install --save rimraf
``

Plus add two scripts to your **package.json** - a build script and a start script. The build script takes all of the files in your root and outputs a compiled version in the dist folder, ignoring the folders and files you'e specified. The start script then builds and runs the code.

```
"build": "rimraf dist/ && babel ./ --out-dir dist/ --ignore ./node_modules,./.babelrc,./package.json,./npm-debug.log --copy-files",
"start": "npm run build && node dist/index.js"
```

You can now rewrite your **index.js** file in es6:

```
import express from 'express';
const app = express();

app.get('/', (req, res) => {
  res.send('Hello world!');
});

app.listen(3000, () => {
  console.log('app listening on port 3000');
});
```

Run `` npm start `` in order to compile and run your node app, and open http://localhost:3000/ in order to see the page loaded, showing 'Hello world!'.

## 3. Start testing your app

Install Mocha:

``npm install --save-dev mocha``

Create a new **test** directory and **test.js** file. In this file, start with a test that you know is going to pass:

```
var assert = require('assert');

describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal(-1, [1,2,3].indexOf(4));
    });
  });
});

```

Here you're going to need to use ES5 for now since Babel does not compile your tests.

Now, add a new test script to your **package.json**:
```
"scripts": {
  "test": "mocha",
  "build": "rimraf dist/ && babel ./ --out-dir dist/ --ignore ./node_modules,./.babelrc,./package.json,./npm-debug.log --copy-files",
  "start": "npm run build && node dist/index.js"
},
```

Now you can run ``npm test`` in the terminal to see your fake test pass:

```
$ npm test

Array
    #indexOf()
      ✓ should return -1 when the value is not present


  1 passing (9ms)

```
