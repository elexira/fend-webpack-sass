# my notes: instructions

Instructions to Follow

As we will start the Express server on a different port, we have to make familiar changes in the webpack.prod.js. Add the rule for sass files, like below:

             {
                 test: /\.scss$/,
                 use: [ 'style-loader', 'css-loader', 'sass-loader' ]
             }

In webpack.prod.js as well as webpack.dev.js, add a new section in module.exports as:

    output: {
         libraryTarget: 'var',
         library: 'Client'
     },

In client/index.js, add the export statement:

    export {
     checkForName,
     handleSubmit
    }

In client/views/index.html, confirm that the custom handleSubmit() function references the newly created Client library, as:

             <section>
                 <form class="" onsubmit="return Client.handleSubmit(event)">
                     <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                     <input type="submit" name="" value="submit" onclick="return Client.handleSubmit(event)" onsubmit="return handleSubmit(event)">
                 </form>
             <section>

In client/js directory, confirm that the javascript function calls refer to the Client library. In formHandler.js:

    Client.checkForName(formText)

Change the port number in the fetch request in the formHandler.js to 8081:

     fetch('http://localhost:8081/test')
     .then(res => {
         return res.json()
     })
     .then(function(data) {
         document.getElementById('results').innerHTML = data.message
     })

Change the port number in server/index.js to 8081 as well:

    // designates what port the app will listen to for incoming requests
    app.listen(8081, function () {
     console.log('Example app listening on port 8081!')
    })

Open two terminal, one for the webpack dev server, and another for Express in production mode. In terminal 1, run the following commands:


    npm install

Optional installation for development mode
    
    npm i -D @babel/core @babel/preset-env babel-loader
    npm i -D style-loader node-sass css-loader sass-loader
    npm i -D clean-webpack-plugin
    npm i -D html-webpack-plugin

Build and start the webpack dev server at port 8080. I think this is 
the app web UI 
    
    npm run build-dev

In terminal 2, run the following commands. I think this is a server API
which usually should be replaced by another API

    # generate a `dist` folder for prod
    npm run build-prod
    # Run the Express server on port 8081
    npm start 




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
