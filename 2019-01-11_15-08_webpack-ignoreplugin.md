---
tags:
  - Webpack  IgnorePlugin
---
利用Webpack的IgnorePlugin插件移除不必要的模块。


Example of ignoring Moment Locales 
As of moment 2.18, all locales are bundled together with the core library (see this GitHub issue).

The resourceRegExp parameter passed to IgnorePlugin is not tested against the resolved file names or absolute module names being imported or required, but rather against the string passed to require or import within the source code where the import is taking place. For example, if you're trying to exclude node_modules/moment/locale/*.js, this won't work:

-new webpack.IgnorePlugin(/moment\/locale\//);
Rather, because moment imports with this code:

require('./locale/' + name);
...your first regexp must match that './locale/' string. The second contextRegExp parameter is then used to select specific directories from where the import took place. The following will cause those locale files to be ignored:

new webpack.IgnorePlugin({
  resourceRegExp: /^\.\/locale$/,
  contextRegExp: /moment$/
});
...which means "any require statement matching './locale' from any directories ending with 'moment' will be ignored.