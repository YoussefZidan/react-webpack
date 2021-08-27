## Creating React Application with Webpack.

In this Article we will learn how to create a React App with Webpack 5.

### 1. Create a folder and initialize NPM

```
npm init -y
```

### 2. Install the following packages

```
npm i react react-dom
```

```
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader html-webpack-plugin sass sass-loader style-loader url-loader webpack webpack-cli webpack-dev-server
```

### 3. Create `.babelrc` file

.babelrc

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

### 4. Create `webpack.config.js` file

webpack.config.js

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  output: {
    path: path.join(__dirname, "/dist"), // the bundle output path
    filename: "bundle.js", // the name of the bundle
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html", // to import index.html file inside index.js
    }),
  ],
  devServer: {
    port: 3030, // you can change the port
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/, // .js and .jsx files
        exclude: /node_modules/, // excluding the node_modules folder
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.(sa|sc|c)ss$/, // styles files
        use: ["style-loader", "css-loader", "sass-loader"],
      },
      {
        test: /\.(png|woff|woff2|eot|ttf|svg)$/, // to import images and fonts
        loader: "url-loader",
        options: { limit: false },
      },
    ],
  },
};
```

### 5. Creating `/src` folder

```
- src
  - App.js
  - App.scss
  - index.html
  - index.js
```

App.js

```js
import React from "react";
const App = () => {
  return <h1>Hello React</h1>;
};

export default App;
```

App.scss

```scss
h1 {
  color: red;
}
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React with Webpack</title>
  </head>
  <body>
    <div id="app"></div>

    <!-- Notice we are pointing to `bundle.js` file -->
    <script src="bundle.js"></script>
  </body>
</html>
```

index.js

```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./App.scss";

const el = document.getElementById("app");

ReactDOM.render(<App />, el);
```

### 6. Creating Scripts

In your `package.json` file add the following

```json
  //....
  "scripts": {
    "serve": "webpack serve --mode development",
    "build": "webpack --mode production"
  },
  //....

```

### 7. Run and modify your App

Run the app with `npm run serve`.
Open your browser on `http://localhost:3030/`
Try to modify and see the changes on the fly.

### 8. Build the App

Run `npm run build`

you will see the following output

```
- dist
  - bundle.js
  - bundle.js.LICENSE.txt
  - index.html
```

**Follow me on**

 <a href="https://www.linkedin.com/in/youssefzidan/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?&style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn">
</a>
