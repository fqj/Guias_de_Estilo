# Integration tasks, construction and deployment

The Angular2 basic project uses Webpack as assets bundler and deployment package optimizer in order to achieve the maximum performance and use the optimal build for each environment. The webpack config tasks can be found in [angular2-basic/config](https://github.com/serenity-frontstack/angular2-basic/tree/master/config). This process includes task such as:

 - Assets bundling
 - Tree shaking to remove unused code
 - SaSS compilation
 - Image optimization
 - Ahead of Time (AoT) compilation

New loaders and plugins can be loaded for different environments on the same previous route. There are three existing environments expected on this process:

 - [Test environment](https://github.com/serenity-frontstack/angular2-basic/blob/master/config/webpack.test.js)
 - [Dev environment](https://github.com/serenity-frontstack/angular2-basic/blob/master/config/webpack.dev.js)
 - [Pro environment](https://github.com/serenity-frontstack/angular2-basic/blob/master/config/webpack.prod.js)

 Those properties files merge their loaders and entry points with the [Common Webpack configuration](https://github.com/serenity-frontstack/angular2-basic/blob/master/config/webpack.common.js). There is another specific properties file for [AoT Compilation](https://github.com/serenity-frontstack/angular2-basic/blob/master/config/webpack.aot.js)

This process can be launched with the following command

    npm run build

This document has the objective of explain the process and configurations allowed in this build

## Webpack common options

- [entry](https://webpack.js.org/configuration/entry-context/#entry): Defines the output modules of the webpack process. It will create one file for each register in this object. In this case we specify three main modules: main, vendor and polyfills. Each of these entry points specifies a file that contains the exports of every modules needed for the application core.
    - main.browser.ts: Contains the main bootstraping of the application. It will create a bundle with all our custom Angular 2 code.
    - vendor.browser.ts: Contains all the dependencies of the application to be deployed, such as Angular libraries, or rxjs modules.
    - polyfills.browser.ts: Contains all the polyfills required by Angular 2 to work with modern browsers without es6 support

- [resolve](https://webpack.js.org/configuration/resolve/): Options affecting the resolving of modules. In our webpack common has the following options
    - [extensions](https://webpack.js.org/configuration/resolve/#resolve-extensions): specify what kind of extensions can be used by the modules. In our case, and because we are using TypeScript, it will has the following value: "['.ts', '.js', '.json']"
    - [modules](https://webpack.js.org/configuration/resolve/#resolve-modules): Specifies the directory where the modules will be found when resolving modules. In our conf will be: [helpers.root('src'), 'node_modules']. We add node_modules because of the use of external modules.
    - [alias](https://webpack.js.org/configuration/resolve/#resolve-alias): This option allows the developer to add an alias for a certain module, in order to import it easily. For example:

            "myAlias": path.resolve(__dirname, '../src/app/shared')   // Allows the developer to use "Import MySharedModule from myAlias/MySharedModule" instead of  "Import MySharedModule from src/app/shared/MySharedModule"
- [module](https://webpack.js.org/configuration/module/): A Module makes reference to every "Import" in our code. Every module imported will be resolved by Webpack following the rules specified in this document.
    - [rules](https://webpack.js.org/configuration/module/#module-rules): An array of rules. Rules modify how the module is created, based on the properties specified. For example:

            {
              test: /\.ts$/,   // Specify the extension for the files to be affected by this rule
              loaders: [       // Specify the loaders to be used resolvin the modules with the extension below
                'awesome-typescript-loader',
                'angular2-template-loader',
                'angular2-router-loader'
              ],
              exclude: [/\.(spec|e2e)\.ts$/]  // Exclusion rules for specific rules, in this case, the unit and e2e tests
            }
         [Loaders](https://webpack.js.org/concepts/loaders/): Loaders are transformations that are applied on a resource file of your application. In the example below, we use some custom loaders for route and template modules resolve

- [plugins](https://webpack.js.org/configuration/plugins/#plugins): Plugins can modify the webpack build process in order to multiple configurations. In our configuration, we use the following plugins:
    - [CommonsChunkPlugin](https://github.com/webpack/docs/wiki/optimization#multi-page-app): Identifies and join common dependencies in a common chunk module
    - [CopyWebpackPlugin](https://www.npmjs.com/package/copy-webpack-plugin): Used for move files to dist directory or assets
    - [HtmlWebpackPlugin](https://github.com/ampedandwired/html-webpack-plugin): This plugin will generate a index.html HTML5 file for you that includes all your webpack bundles in the body using script tags, following the specified options
    - [ScriptExtHtmlWebpackPlugin](https://github.com/numical/script-ext-html-webpack-plugin): Adds the defer attribute to script tags in the HTML autogenerated file, in order to improve the first paint of the application
    - HtmlElementsPlugin: Provides access to head-config.common modules through <%= webpackConfig.htmlElements.headTags %> in an html file
    - [LoaderOptionsPlugin](https://gist.github.com/sokra/27b24881210b56bbaff7): Can be configured to minimize, test or start debug mode in the module resolving

# Webpack production options

At the beggining of the webpack production file we can see the following

    const METADATA = webpackMerge(commonConfig({env: ENV}).metadata, {
      host: HOST,
      port: PORT,
      ENV: ENV,
      HMR: false
    });

This set the environment variables to the specified values. If we run the npm run build command, by default it runs build task with the  --config config/webpack.prod.js parameter. The HOST, PORT and ENV can be setted in order to your needed configuration. Or more easily and naturally, **modifying the config/app.config.json**
After this, the module resolving process starts after merge the production configuration with the commons configuration. In this process some options are added:

- [output](https://webpack.js.org/configuration/output/): Specifies the output of the process. The objective here is generate a dist directory with the **production-ready** app
    -   [path](https://webpack.js.org/configuration/output/#output-path): Specifies the output directory for the production app, in our case, will be **"dist"**
    -   [filename](https://webpack.js.org/configuration/output/#output-filename): Specifies the name of the output modules, based on the entry points defined on the common configuration. We will use expressions in order to obtain a generated filename for each file. [name].[chunkhash].bundle.js will generate a file with the entry point name, followed by a random hash, and a bundle.js extension
    -   [sourceMapFilename]( http://webpack.github.io/docs/configuration.html#output-sourcemapfilename): Specifies the name of the output modules sourceMap
    -   [chunkFilename](http://webpack.github.io/docs/configuration.html#output-chunkfilename): Specifies the name of the output chunks, in our case, the lazy load modules that will be loaded dynamically, or the common dependencies.

- Plugins: We added some plugins configuration in order to optimize the production build
    -   [WebpackMd5Hash](https://www.npmjs.com/package/webpack-md5-hash): Replace the chunkhash method generation with md5 algorithm
    -   [DefinePlugin](https://webpack.github.io/docs/list-of-plugins.html#defineplugin): Take the passed environment variables making them accessible for the developers via js
    -   [UglifyJsPlugin](https://webpack.js.org/guides/production-build/#minification): Allows us to uglify the code automatically
