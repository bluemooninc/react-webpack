# React, Webpack4, Babel7 12 step to start-up your project

Here, I'll explain the environment construction from initialization of npm to displaying Hello world with React in 12 steps.

## 1.Make work dir and init npm

Create working dir and init your project.
```bash
mkdir react-webpack
cd react-webpack
## some question will occur for init your project. Its' okay to retuen all.
npm init
```

## 2.Install react module
```text
npm i react react-dom
```
## 3.Install Webpack 4
Install webpack files on project folder. 
```text
$ npm i --save-dev webpack webpack-dev-server webpack-cli
```

## 4.Install Babel 7

Install babel files on project folder.
```text
$ npm i --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader html-webpack-plugin
```

Check the node module versions
```
$ npm list --depth=0
  react-webpack@1.0.0
  ├── @babel/core@7.6.0
  ├── @babel/preset-env@7.6.0
  ├── @babel/preset-react@7.0.0
  ├── babel-loader@8.0.6
  ├── babel-preset-react@6.24.1
  ├── html-webpack-plugin@3.2.0
  ├── react@16.9.0
  ├── react-dom@16.9.0
  ├── webpack@4.40.2
  ├── webpack-cli@3.3.9
  └── webpack-dev-server@3.8.1
```

## 5.Edit webpack config

touch webpack.config.js and insert below code.
```text
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    mode: 'development',
    entry: [
        './src/index.js'
    ],
    output: {
        path: path.join(__dirname + '/dist'),
        filename: 'bundle.js'
    },
    module: {
        rules: [{
            test: /\.(js|jsx)$/,
            exclude: /node_modules/,
            use: [
                {
                    loader: 'babel-loader',
                    options: {
                        presets: [['@babel/preset-env', { modules: false }]]
                    }
                }
            ]
        }]
    },
    resolve: {
        extensions: ['.js', '.jsx'] // use js, jsx file
    },
    devServer: {
        open: true,
        historyApiFallback: true,
        contentBase: path.join(__dirname, '/dist'),
        watchContentBase: true,
        inline: true,
        hot: true,
    },
    plugins: [
        new HtmlWebpackPlugin({
            title: 'Custom template',
            template: 'src/index.html'
        })
    ]
};
```

## 6.Edit index.html

touch src/index.html and insert below code.
```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>My Document</title>
</head>
<body>
<h1>Start Ok</h1>
<div id="app"></div>
</body>
</html>
```
## 7.Edit .Babelrc
```text
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## 8.Edit index.js
touch src/index.js and insert below code.
```text
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('app'));
```

## 9.Edit App.js

touch src/App.js and insert below code.
```text
import React from 'react';

export default class extends React.Component {
    render() {
        return (
            <div>
                <h1>Hello World!</h1>
            </div>
        );
    }
}
```

## 10.Edit package.json

insert script setting below
```text
  "scripts": {
    "start": "webpack-dev-server --port 3000",
    "build": "webpack --mode production"
  },
```

## 11.Start local server

this command is start web server and run web browser.
You can see it change when you edit html or js files.
```text
npm run start
```

## 12.Build webpack

It's gonna production files to web server. 

```text
npm run build
```