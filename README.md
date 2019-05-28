# webpack-source
example basic setup of webpack with source mapping for error tracing

1. Run following 3 commands:

```
npm init -y
npm install webpack --save-dev
npm install webpack-cli --save-dev

```

2. create .gitignore file, to ignore node modules - see file.

3. Create 'src' folder, and add index.js to it. + Create 'dist' folder and add index.html + main.js to it. (see files/folders). At this point, a simple 'hello world' message in index.html + a DOM manipulation 'hello world' in index.js, is sufficient for testing.

4. change line in package.json (to "prevent accidental publish of your code"):

```
+   "private": true,
-   "main": "index.js",
```

5. run <code>npx webpack</code>

6. Open index.html in browser and check 'hello world' messages are functioning.

7. Note that <code>npx webpack --watch</code> will now avoid needing to run </code>npx webpack</code> after every change made.

8. Module pattern (using separate file(s) and export / import statements), now works, but add webpack.config.js for good measure:
```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```
9. Introduce error in either index.js or aModule.js, and note lack of tracing in error message:
```
Uncaught ReferenceError: x is not defined
    at Module.<anonymous> (main.js:1)
    at n (main.js:1)
    at main.js:1
    at main.js:1
```

10. Add <code>mode: 'development'</code> and <code>devtool: 'inline-source-map'</code> to webpack.config.js, to give:
```
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  devtool: 'inline-source-map',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  }
};
```

11. Error stack trace should now work in browser console. E.g:
```
Uncaught ReferenceError: x is not defined
    at aModule (aModule.js:5)
    at Module../src/index.js (index.js:7)
    ...
```

NOTE: This example also includes addition of <code>"build": "webpack"</code> line to package.json (see file), to enable the <code>npm run build</code> command (alias for <code> npx webpack</code>). This is not necessary for the source-mapping feature to work.
