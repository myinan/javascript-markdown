# Webpack
### (How to use / Workflow to follow)
---
### [Webpack Documentation Getting Started Guide](https://webpack.js.org/guides/getting-started/)

### [Webpack Documentation Asset Management Guide](https://webpack.js.org/guides/asset-management/)

### [Install html-webpack-plugin and use a custom template with html-webpack-plugin](https://rapidevelop.org/webpack/setup-html-webpack-plugin)

### [Webpack Documentation Output Management Guide](https://webpack.js.org/guides/output-management/)

+ This tutorial on output management also gives an example of using html-webpack-plugin but does not demonstrate using the template option. It also starts by demonstrating how to configure multiple entry points - you are unlikely to need this feature for the projects in this part of the course.

### [Webpack Documentation Development Guide](https://webpack.js.org/guides/development/)

+ The first part of this tutorial (up until “Choosing a Development Tool”) talks about source maps, a handy way to track down which source file (index.js, a.js, b.js) an error is coming from when you use webpack to bundle them together. This is essential to debugging bundled code in your browser’s DevTools. If the error comes from b.js the error will reference that file instead of the bundle. It also walks through an example of the --watch feature and webpack-dev-server package, either of which will prove invaluable when working with webpack.

+ Note that if you decide to use webpack-dev-server, the tutorial example sets it to serve from dist. If you are using html-webpack-plugin, you will want to change this to serve from src instead. This will make development much easier as all of your work and any file paths you use can be kept within src (Webpack will adjust all of these file paths when bundling if you set the correct loaders and asset rules).

+ You can ignore the last option (webpack-dev-middleware) as we will not be working with our own Express server for this part of the course.

#### **Development Workflow with webpack-dev-server:**
   - During the development phase, you use `webpack-dev-server` with the development server serving from the "src" directory.
   - This allows for a fast and efficient development experience. The bundled files are kept in memory (RAM), and webpack-dev-server automatically reloads your application as you make changes to your source code.

**Optimized Production Build:**
   - Once your application reaches a mature state and you are ready to deploy it to production, you trigger the production build using a command like `npm run build`.
   - This command invokes the webpack build process with a production configuration, which includes optimizations such as minification, tree shaking, and other performance enhancements.

**Output to Hard Disk:**
   - The production build generates the optimized and bundled files, and they are written to the specified output directory on the hard disk (commonly "dist").
   - This directory (`dist`) now contains the final version of your application that is suitable for deployment.

This workflow is advantageous because it prioritizes speed and convenience during development by using `webpack-dev-server` and serving from memory. When it comes time to deploy the application, you switch to a production build that ensures optimized and minified code is written to disk for improved performance in a production environment.

By having a clear separation between development and production configurations, you can balance the need for quick development iterations with the requirements of a performant and efficient production deployment.

### [Webpack Documentation Production Guide](https://webpack.js.org/guides/production/)
+ Setting our webpack configuration to development mode is naturally most suitable for our development work, but when we come to build our projects for deployment (production), the dedicated production mode optimises this for us. Instead of manually switching between modes in the configuration file as needed, this tutorial introduces webpack-merge. This can be quite useful as a quick setup allow us to have a dedicated npm script for development builds/dev server, and another specifically for our production build.

+ You’ll notice the above tutorial does not have a webpack.config.js file. If you do use webpack-merge, make sure that any webpack commands you run (including in an npm script) follow the tutorial and use the --config option to specify which webpack configuration file to use. If you do not specify one, webpack will try to look for webpack.config.js and if it does not find one, it will not be able to bundle correctly!

### [Webpack Documentation // Guides](https://webpack.js.org/guides/)
+ You don’t need to do the rest of the webpack tutorials at this time, but take a look at what’s offered on the sidebar of their guides page. There are several sweet features that you may want to use in future projects such as code-splitting, lazy-loading, and tree-shaking, so being aware of some of these features can come in handy. Now that you have a handle on webpack’s configuration system adding these features is as easy as using the right plugins and loaders!

---
### Knowledge Check

**Q1.** How do you load CSS using webpack?

**A1.** In order to `import` a CSS file from within a JavaScript module, you need to install and add the style-loader and css-loader to your module configuration:

```npm install --save-dev style-loader css-loader```

```js
// webpack.config.js

 const path = require('path');

 module.exports = {
   entry: './src/index.js',
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist'),
   },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
 };
```

Module loaders can be chained. Each loader in the chain applies transformations to the processed resource. A chain is executed in reverse order. The first loader passes its result (resource with applied transformations) to the next one, and so forth. Finally, webpack expects JavaScript to be returned by the last loader in the chain.

The above order of loaders should be maintained: 'style-loader' comes first and followed by 'css-loader'. If this convention is not followed, webpack is likely to throw errors.

webpack uses a regular expression to determine which files it should look for and serve to a specific loader. In this case, any file that ends with .css will be served to the style-loader and the css-loader.

This enables you to `import './style.css'` into the file that depends on that styling. Now, when that module is run, a \<style> tag with the stringified css will be inserted into the \<head> of your html file.

```js
// index.js
import './style.css';

// Rest of the code...
```

Loaders exist for pretty much any flavor of CSS you can think of – postcss, sass, and less to name a few.

**Q2.** How do you load images using webpack?

**A2.** As of webpack 5, using the built-in `Asset Modules` we can easily incorporate images like backgrounds and icons in our system as well:

```js
// webpack.config.js

 const path = require('path');

 module.exports = {
   entry: './src/index.js',
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist'),
   },
   module: {
     rules: [
       {
         test: /\.css$/i,
         use: ['style-loader', 'css-loader'],
       },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
     ],
   },
 };
```

Now, when you `import MyImage from './my-image.png'`, that image will be processed and added to your output directory and the `MyImage` variable will contain the final url of that image after processing. When using the css-loader, as shown above, a similar process will occur for url('./my-image.png') within your CSS. The loader will recognize this is a local file, and replace the './my-image.png' path with the final path to the image in your output directory. The html-loader handles \<img src="./my-image.png" /> in the same manner.

```js
// src/index.js

import _ from 'lodash';
import './style.css';
import Icon from './icon.png';

function component() {
   const element = document.createElement('div');

   element.innerHTML = _.join(['Hello', 'webpack'], ' ');
   element.classList.add('hello');

   // Add the image to our existing div.
   const myIcon = new Image();
   myIcon.src = Icon;

   element.appendChild(myIcon);

   return element;
}

document.body.appendChild(component());
```

```css
/* src/style.css */

.hello {
color: red;
background: url('./icon.png');
}
```

You'll see that the actual filename in `./dist` has changed to something like 29822eaa871e8eadeaa4.png. This means webpack found our file in the src folder and processed it.

**Q3.** How do you load fonts using webpack?

**A3.** The built-in `Asset Modules` will take any file you load through them and output it to your build directory. This means we can use them for any kind of file, including fonts. Let's update our webpack.config.js to handle font files:

```js
 // webpack.config.js

 const path = require('path');

 module.exports = {
   entry: './src/index.js',
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist'),
   },
   module: {
     rules: [
       {
         test: /\.css$/i,
         use: ['style-loader', 'css-loader'],
       },
       {
         test: /\.(png|svg|jpg|jpeg|gif)$/i,
         type: 'asset/resource',
       },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
     ],
   },
 };
```
With the loader configured and fonts in place, you can incorporate them via an `@font-face` declaration. The local url(...) directive will be picked up by webpack, as it was with the image:

```css
/* src/style.css */

@font-face {
  font-family: 'MyFont';
  src: url('./my-font.woff2') format('woff2'),
  url('./my-font.woff') format('woff');
  font-weight: 600;
  font-style: normal;
}

.hello {
  color: red;
  font-family: 'MyFont';
  background: url('./icon.png');
}
```


**Q4.** How do you automatically build HTML files in dist using webpack?

**A4.** First install the plugin and adjust the webpack.config.js file:

```npm install --save-dev html-webpack-plugin```

```js
// webpack.config.js

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
   entry: {
     index: './src/index.js',
   },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      inject: 'head',
      scriptLoading: 'defer',
      filename: 'index.html',
    }),
  ],
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist'),
  },
};
```

Before we do a build (`npm run build`), you should know that the `HtmlWebpackPlugin` by default will generate its own index.html file, even if we already have one in the dist/ folder. This means that it will replace our index.html file with a newly generated one.

In order to use a "template" html file, we have declared a template property on our HtmlWebpackPlugin's argument object with the value './src/index.html'. This way whenever we do a build, HtmlWebpackPlugin will use our source html file as it's template. 

**Q5.** How do you automatically build an HTML file in dist using a custom template in src?

**A5.** As explained above, in order to use a "template" html file, we have to declare a template property on our HtmlWebpackPlugin's argument object and set it's value to './src/index.html'. This way whenever we do a build, HtmlWebpackPlugin will use our source html file as it's template.

**Q6.** How would you track errors in bundled source code?

**A6.**  When webpack bundles your source code, it can become difficult to track down errors and warnings to their original location. For example, if you bundle three source files (a.js, b.js, and c.js) into one bundle (bundle.js) and one of the source files contains an error, the stack trace will point to bundle.js. This isn't always helpful as you probably want to know exactly which source file the error came from.

In order to make it easier to track down errors and warnings, JavaScript offers `source maps`, which map your compiled code back to your original source code. If an error originates from b.js, the source map will tell you exactly that.

For development, we can use the `inline-source-map` option.

```js
// webpack.dev.js
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
   mode: 'development',
   devtool: 'inline-source-map', // <<----
   devServer: {
     static: './src',
   },
   module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
    ],
  },
});
```