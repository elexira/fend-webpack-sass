# my notes

Add Service Workers

Google Workbox makes working with basic Service Workers incredibly convenient. We are going to follow their setup instructions, the steps are going to feel very familiar by now, because Google Workbox created a webpack plugin for us.

We are going to add service workers to webpack.prod.js config file, because to allow offline access, what the service workers actually do is create a cached version of your website that they can supply if the server can’t be reached. But we don’t want that caching around our dev site, so we won’t add this to our dev config at all.

Like we’ve learned with most plugins, when we call the generate service workers function, we have the ability to pass in some options. There are lots of cool options you can choose from, to do things like cache images at runtime, limit the max size of your cache, etc. For now, we are going to stick with the default settings.

So, we do our three steps:

In webpack.prod.js config file,
Require the plugin, by appending the new plugin statement

        const WorkboxPlugin = require('workbox-webpack-plugin');

Instantiate the new plugin in the plugin list:

        new WorkboxPlugin.GenerateSW()

On the terminal, install the plugin using npm install workbox-webpack-plugin --save-dev

If you follow along with the [Workbox Service Worker documentation](https://developers.google.com/web/tools/workbox/guides/generate-service-worker/webpack), there’s one more step. We need to register a Service Worker with our app. To do this, we will add a script to our /src/client/views/index.html file and call the register service worker function if the browser supports service workers.

Add this code to the bottom of your html file, just above the closing body tag.

    <script>
     // Check that service workers are supported
     if ('serviceWorker' in navigator) {
         // Use the window load event to keep the page load performant
         window.addEventListener('load', () => {
             navigator.serviceWorker.register('/service-worker.js');
         });
     }
    </script>




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
