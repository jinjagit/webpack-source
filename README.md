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
