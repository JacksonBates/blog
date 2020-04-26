---
layout: default
title: Fixing AntD CSS Module Imports in Create React App with CRACO
permalink: /antd-craco-shenanigans
---

In trying to speed up one of the inherited sites I maintain at work, I aimed to do the reasonably simple task of chunking CSS in a Create React App.

It became clear quite quickly that the stylesheet for AntD was all being loaded at once, and fixing this is supposed to be quite easy, according to AntD's documentation.

In theory, AntD uses ES6 tree-shaking to only load the required CSS, when configured correctly. Normally this is handled with a webpack plugin, [babel-plugin-import](https://github.com/ant-design/babel-plugin-import), but obviously this is complicated a little by Create React App, which abstracts away the webpack config.

AntD recommend using react-app-rewired and customize-cra in their [Advanced Guide](https://ant.design/docs/react/use-with-create-react-app#Advanced-Guides).

After removing the initial vendor stylesheet loading left behind by the previous developers, the configuration suggested by AntD did work, and shaved 500kb off the initial CSS download.

However, CI was failing due to build warnings, so this could not be deployed.

The culprit was MiniCssExtractPlugin, which complains about [Conflicting order](https://github.com/facebook/create-react-app/issues/5372). There are a number of Github issues about this.

Ultimately, to fix this I determined that since the CSS order was not causing actual problems on the site, it was safe to silence those particular warnings. To do this, you can add the ignoreOrder option to MiniCssExtractPlugin in the webpack config.

Unfortunately, the existing webpack config already has a reference to this and sets the ignoreOrder option to false.

I decided to use CRACO (Create React App Config Override) instead of React App Rewired, since the config syntax is more similar to a real webpack config, and it allows you to use the existing webpack config directly to build your updated version.

My final code in the craco.config.js looks like this:

```
const CracoAntDesignPlugin = require("craco-antd");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  webpack: {
    configure: (webpackConfig, { env, paths }) => {
      webpackConfig = {
        ...webpackConfig,
        plugins: [
          ...webpackConfig.plugins.filter((element) => {
            if (element.options) {
              return !element.options.hasOwnProperty("ignoreOrder");
            }
            return true;
          }),
          new MiniCssExtractPlugin({
            filename: "static/css/[name].[contenthash:8].css",
            moduleFilename: this.moduleFilename,
            ignoreOrder: true,
            chunkFilename: "static/css/[name].[contenthash:8].chunk.css",
          }),
        ],
      };
      return webpackConfig;
    },
  },
  plugins: [{ plugin: CracoAntDesignPlugin }],
};
```

The 'craco-antd' plugin does the same as the babel-import-plugin suggested by AntD - it's just a simpler plugin version designed to work with CRACO.

The part of this config I really want to improve is the naive filter for targeting the MiniCssExtractPlugin. You can see in the code above that I build the webpack config by spreading the original webpack config, and spreading the existing plugins, except for the one that has the "ignoreOrder" property, then I can add my own MiniCssExtractPlugin config at the end of the plugins array.

However, this works for now and the much slimmer version of the app is happily deployed.

This was, upon reflection, a lot of messing around to avoid ejecting the app, but I think the long term gains of being able to keep an easier to upgrade CRA, and all the perf and tooling work done behind the scenes with react-scripts, will vindicate this decision.

{% include twitter_plug.html %}
