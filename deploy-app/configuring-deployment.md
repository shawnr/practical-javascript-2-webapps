# Configuring Deployment

To configure the deployment of our Vue.js application, we will leverage the ability of Github Pages to serve a website from the `docs` folder in a project repository. This means that we need to alter our configuration so that Webpack builds the code into the `docs/` directory instead of the `dist/` directory (which is the default location Webpack uses). 

To make this happen we will need to modify the Webpack configuration in `config/index.js`. The default configuration looks like this. (Note: there may be some extra comments in the code that was generated from the Vue-CLI.)

```js
var path = require('path')

module.exports = {
  build: {
    env: require('./prod.env'),
    index: path.resolve(__dirname, '../dist/index.html'),
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    productionSourceMap: true,
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],
    bundleAnalyzerReport: process.env.npm_config_report
  },
  dev: {
    env: require('./dev.env'),
    port: 8080,
    autoOpenBrowser: true,
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {},
    cssSourceMap: false
  }
}
```

In this code we can see that there is a `build` configuration and a `dev` configuration. These configurations are used by `npm` when we run the `build` or `dev` command. When we execute `npm run build`, it is building the site using the configuration defined above. We can see that configuration refers to the `dist/` directory. In order to make this work on Github Pages, we need to alter that to refer to the `docs/` directory.

In addition, we must change the `assetsPublicPath` value because it currently points to `'/'`. The "forward slash" is an absolute URL that will break on Github Pages (because our projects on Github Pages are always served in a subdirectory). We can fix this by changing the value to nothing (`''`) or to the "dot-slash" (`'./'`), which would be relative to the subdirectory.

Here is what the `config/index.js` file looks like after we make these changes:

```js
var path = require('path')

module.exports = {
  build: {
    env: require('./prod.env'),
    index: path.resolve(__dirname, '../docs/index.html'),
    assetsRoot: path.resolve(__dirname, '../docs'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '',
    productionSourceMap: true,
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],
    bundleAnalyzerReport: process.env.npm_config_report
  },
  dev: {
    env: require('./dev.env'),
    port: 8080,
    autoOpenBrowser: true,
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {},
    cssSourceMap: false
  }
}
```

Once we have made those changes to the `config/index.js` file, we can run the commands to build and deploy the site.






