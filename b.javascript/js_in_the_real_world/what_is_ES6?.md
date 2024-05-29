# What is ES6?
ES6 is a version of JavaScript that was officially released in the summer of 2015. It included many new features that make writing JavaScript much easier and cleaner. If you have been following our lessons you have already been learning these new features because, well, ES6 is just *JavaScript*.

You have probably also come across articles talking about features in ES7 or ES8 or ES2015 or ES2017 etc. Part of the confusion here is that right after the release of ES6, the committee that makes these decisions changed the naming scheme from ‘version numbers’ (ES4, ES5, ES6 etc.) to ‘release years’ (ES2016, ES2017, ES2018 etc.)

To clear any confusion left regarding the difference between Javascript and ECMAScript, here’s what happened long, long ago:

+ JavaScript was originally named JavaScript in hopes of capitalizing on the success of Java.
+ Netscape then submitted JavaScript to ECMA International for Standardization. (ECMA is an organization that standardizes information)
+ This results in a new language standard, known as ECMAScript.
+ Put simply, ECMAScript is a standard. While JavaScript is the most popular implementation of that standard. JavaScript implements ECMAScript and builds on top of it.

#### Okay, so ‘ES’…?
ES is simply short for ECMAScript. Every time you see ES followed by a number, it is referencing an edition of ECMAScript. In fact, there are eight editions of ECMAScript published. Lets dive into them:

#### ES1, ES2, ES3, ES4
ES1: June 1997 — ES2: June 1998 — ES3: Dec. 1999 — ES4: Abandoned

I’ve grouped all of these together. These were the first 4 editions of ECMAScript, and to save time, we wont go too in-depth. Just know that the first three editions were annual, and the fourth was abandoned due to political differences.

#### ES5
December 2009: Nearly 10 years later, ES5 was released in 2009. It would then take almost six years for the next version of ECMAScript to be released.

#### ES6 / ES2015
June 2015: Perhaps the cause for all of your confusion begins here. You see, ES6 and ES2015 are the same thing.

ES6 was the popularized name prior to release. However, the committee that oversees ECMAScript specifications made the decision to move to annual updates. With this change, the edition was renamed to ES 2015 to reflect the year of release. Subsequent releases will therefor also be named according to the year they are released.

#### ES2016 (ES7)
June 2016: Seventh edition of ECMAScript.

#### ES2017 (ES8)
June 2017: Eighth edition of ECMAScript.

.<br>
.<br>
.<br>

#### ES.Next
You may have also seen ES.Next used online. This term is dynamic and references the next version of ECMAScript coming out.

#### Key Takeaways:
+ Each release brings updates and new features to the language.
+ An update to ECMAscript can be expected annually.
+ Initial Editions of ECMAScript are named numerically, increasing by 1: ES1, ES2, ES3, ES4, ES5.
+ New editions (starting with 2015) will be named ES followed by the year of release: ES2015, ES2016, ES2017...
+ ECMAScript is a standard. JavaScript is the most popular implementation of that standard. Other implementations include: `SpiderMonkey`, `V8`, and `ActionScript`.

## Babel
The problem with JavaScript constantly updating and adding features is that it sometimes takes web-browsers a while to catch up and implement new features once they’ve been released. At the current time all modern browsers (Chrome, Firefox, Safari and Edge) support all of ES6, and most of ES7, but older browsers (various versions of Internet Explorer for instance) do not. This means, unfortunately, that if you write code that uses these new features it will not run in browsers that do not support it.

For most of us, this has not been an issue because you are almost definitely using a new browser that automatically updates itself when a new version is released. But in the real world, if you’re selling products to customers you can’t control which browsers people will use to connect to your site.

Fortunately there is a solution to this problem. `Babel` is a tool that takes your modern JavaScript code and **transpiles** it to code that older browsers can understand. It can be used from the command line with a single command, and can also easily be added to your webpack configuration with the babel-loader.

JavaScript is constantly changing, and as new features are announced and released, you can use Babel to try them out, often before they’re available in any browser.

```js
// My webpack.prod.js configuration

const { merge } = require("webpack-merge");
const common = require("./webpack.common.js");

module.exports = merge(common, {
  mode: "production",
  devtool: "source-map",
  module: {
    rules: [
      {
        test: /\.(?:js|mjs|cjs)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: [["@babel/preset-env", { targets: "defaults" }]],
          },
        },
      },
    ],
  },
});
```

1. **Module Rules:**
   ```javascript
   module: {
     rules: [
       // Your rule goes here
     ],
   }
   ```
   In a Webpack configuration, the `module` property is used to define how modules should be treated. Modules are essentially the different types of files in your project, such as JavaScript files, CSS files, images, etc. The `rules` array contains a list of rules that define how different types of files should be processed.

2. **Rule for JavaScript Files:**
   ```javascript
   {
     test: /\.(?:js|mjs|cjs)$/,
     exclude: /node_modules/,
     use: {
       loader: "babel-loader",
       options: {
         presets: [["@babel/preset-env", { targets: "defaults" }]],
       },
     },
   }
   ```
   This rule specifically targets JavaScript files (`.js`, `.mjs`, and `.cjs` extensions). Let's go through each property:

   - **`test`:** This property is a regular expression that is used to match the file extensions that this rule should apply to. In this case, it matches files with `.js`, `.mjs`, or `.cjs` extensions.

   - **`exclude`:** This property specifies directories or files that should be excluded from the rule. In this case, the rule excludes files in the `node_modules` directory. This is common because you typically don't want to transpile or process third-party library code located in `node_modules`.

   - **`use`:** This property specifies the loader and its options that should be used to process the matched files.

     - **`loader`:** The loader is responsible for transforming the matched files. In this case, the `babel-loader` is used. Babel is a JavaScript compiler that can be used to convert modern JavaScript code (ES6 and later) into a version of JavaScript that is compatible with a wider range of browsers.

     - **`options`:** Here, you provide options specific to the loader. In this case, Babel's options are specified. The `presets` option is used to define sets of plugins that Babel should use during the transformation process. `["@babel/preset-env", { targets: "defaults" }]` is a common preset that tells Babel to transpile the code to match the environments specified by the "defaults" browserlist, ensuring compatibility with a broad range of browsers.

In summary, this webpack module rule uses Babel to transpile JavaScript files, excluding those in the `node_modules` directory, and targeting a default set of browser environments.

### Babel plugins and presets
To make Babel actually do something useful, we need to add a plugin. It’s the plugins that does the heavy lifting with Babel. Each plugin is it’s own NPM library. So for every plugin you want to install, you have to install a new NPM library. For example, we can install a Babel plugin that transpiles ES6 arrow functions so that we ensure compatibility with older browsers. But if you want to use more ES6 features you would need to install one NPM package and add an entry in .babelrc for every feature. That’s just too much work. But there is a solution to this: **presets**!

The Babel foundation has created presets that contains common bundles of plugins. That means you only have to do the NPM installation and babel configuration once and then a bunch of plugins are automatically installed for you.

There are many different Babel presets, both official presets from Babel foundation and unofficial presets from other organizations such as Airbnb.

The official presets are:<br>
+ @babel/preset-env
+ @babel/preset-flow
+ @babel/preset-react
+ @babel/preset-typescript

### @babel/preset-env:
`@babel/preset-env` is a Babel preset that enables you to use the latest JavaScript syntax and features without worrying about the specific environments where your code will run. It automatically determines the set of plugins and polyfills needed to make your code compatible with the specified target environments.

By default, babel-preset-env just installs all ES6 plugin you’ll need. But this can quickly bloat up your bundle. We can tell Babel to not use all plugins, but only a subset of plugins that you really need. That way less of your code gets transpiled to bloated ES5 code. We can do this by telling `@babel/preset-env` that which browsers should it target.

When you configure Babel with `["@babel/preset-env", { targets: "defaults" }]`, it essentially means that Babel will transpile your code based on the browsers or environments defined by the "defaults" query in the browserlist.

### Browserlist and "defaults":
Browserlist is a configuration file format and JavaScript API used by various front-end tools to share target environments (browsers or Node.js versions) between different tools. The "defaults" value in the context of Babel and Browserlist refers to a predefined set of target environments that are considered broadly representative of the average global usage.

When you set `targets: "defaults"`, Babel uses the Browserlist "defaults" configuration to determine the browsers or environments for which it should generate compatible code. The "defaults" configuration is often updated based on global usage statistics to reflect the most common browsers in use.

For the most up-to-date information on what is included in the "defaults" configuration, you should refer to the official [Browserlist documentation](https://browserl.ist/) or the [GitHub repository](https://github.com/browserslist/browserslist).

In summary, by using `["@babel/preset-env", { targets: "defaults" }]`, you are instructing Babel to transpile your code to be compatible with the default set of widely used browsers, as defined by the Browserlist "defaults" configuration. This helps ensure broad compatibility without manually specifying a list of specific browsers and their versions.

### Babel enables you to use the latest ECMAScript features
`@babel/preset-env` is designed to allow you to use the latest ECMAScript features without having to worry about whether the environments where your code runs support those features. It dynamically transpiles your code to match the target environments you specify.

When you configure Babel with `["@babel/preset-env", { targets: "defaults" }]` or a similar configuration, it will enable transformations for the ECMAScript features that are not natively supported in the target environments. This includes features from ECMAScript 2023 and beyond.

For example, if ECMAScript 2023 introduces new syntax or features, `@babel/preset-env` will automatically handle the transpilation of your code to ensure compatibility with the specified target environments, even if those environments do not natively support the latest ECMAScript features.

It's important to keep `@babel/preset-env` updated to the latest version to benefit from the most recent transformations and compatibility improvements. You can typically do this by updating your project's dependencies.

Keep in mind that the effectiveness of `@babel/preset-env` depends on the accuracy of the Browserlist targets and the availability of Babel plugins to handle specific language features. Always check the Babel and Browserlist documentation for the latest information and updates.

### `.babelrc` and `.browserlistrc`
With the provided webpack configuration using `@babel/preset-env`, you don't necessarily need separate `.babelrc` and `.browserlistrc` files. The configuration within the `webpack.prod.js` file is often sufficient for many projects.

Here's a recap of why:

1. **Babel Configuration (`@babel/preset-env`):**
   The Babel configuration is included directly in your `webpack.prod.js` file. This is a common practice, especially in simpler projects or when you prefer to keep the configuration centralized.

   ```javascript
   options: {
     presets: [["@babel/preset-env", { targets: "defaults" }]],
   },
   ```

   This configuration specifies that Babel should use the `@babel/preset-env` preset with the "defaults" target, which means it will automatically transpile your code to be compatible with commonly used browsers.

2. **Browserlist Configuration:**
   The `targets: "defaults"` in your Babel configuration is essentially a shortcut for using the default Browserlist configuration. Browserlist, which defines target environments, is implicitly handled by Babel through the `@babel/preset-env` preset.

If your project needs more granular control over the list of target environments, or if you want to manage the Browserlist configuration separately, you might consider using a separate `.browserlistrc` file. Similarly, if you have additional Babel plugins or configurations, you might consider a separate `.babelrc` or `babel.config.js` file.

In conclusion, for many projects, having the Babel and Browserlist configurations within the `webpack.config.js` file simplifies setup and maintenance. However, as your project grows or if you have specific needs, using separate configuration files might become more practical.