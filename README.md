# my notes

Steps Followed in the Demonstration Video

In packages.json append the following new entries in "devDependencies":

    "mini-css-extract-plugin": "^0.9.0",
    "terser-webpack-plugin": "^1.3.0",
    "optimize-css-assets-webpack-plugin": "^5.0.3",

The version may vary with time.

In webpack.prod.js config file, append the new plugin statements:

    const MiniCssExtractPlugin = require('mini-css-extract-plugin');
    const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');
    const TerserPlugin = require('terser-webpack-plugin');

Add the optimization attribute in module.exports section, that will help us to minimize certain files. Notice that the TerserPlugin and OptimizeCSSAssetsPlugin are being initialized here.

    optimization: {
      minimizer: [new TerserPlugin({}), new OptimizeCSSAssetsPlugin({})],
      },

Updated the rule section for Sass file loaders:

    {
    test: /\.scss$/,
    use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"],
    },

Instantiate the new plugin in the plugin list:

    new MiniCssExtractPlugin({ filename: "[name].css" })

On the terminal, run the following commands:

    npm i -D mini-css-extract-plugin
    npm i -D optimize-css-assets-webpack-plugin terser-webpack-plugin
    npm run build-prod


What is the purpose of a .map file?
 
Map files keep track of which source files the code in your bundled file comes from. This is incredibbly handy when debugging. Without a map file, you would get an error that says it is coming from like 1783 of bundle.js - which isn’t very helpful, but with a source map turned on it would tell you the file name and line where the error is occuring. Much better!



# Webbpack Express Example App

The goal of this repo is be an example of a basic but functional app built on Express and Webpack.

If you want to follow along, start from branch 0-initial-setup. Each branch in this project is a step along the path to creating a fully functional webpack setup. In each branch, there will be a documentation file that lists out the steps taken in that branch (each step is also roughly a git commit if you look at the history) which you can use as a checklist when setting up your own projects. 

## What we will cover

We will cover:

- Webpack entry point
- Webpack output and dist folder
- Webpack Loaders
- Webpack Plugins
- Webpack Mode
- Tools for convenient Webpack development

## Get Up and Running

Fork this repo, then clone the branch of your choice from your forked repo down to your computer:

```
git clone -- git@github.com:[your-user-name]/webpack-express.git --
```

`cd` into your new folder and run:
- ```npm install```
- ```npm start``` to start the app
- this app runs on localhost:8080, but you can of course edit that in server.js
