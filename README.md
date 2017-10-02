``
npm init -y
``

``
npm install --save express
``



Then your package.json should look like this:
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


Don't forget to create a .gitignore file to hide your node_modules from git:
```
node_modules
```

Create an index.js file at the root and do a quick configuration of your express app:

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
