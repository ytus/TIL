## Error `/usr/bin/env: ‘node’: No such file or directory` in Webstorm

When running a node package as an _External Tool_ in Webstorm (for example prettier), you can get this error:

> /usr/bin/env: ‘node’: No such file or directory

It may be caused by the way `nvm` changes your `PATH`, see: https://intellij-support.jetbrains.com/hc/en-us/community/posts/205964744-npm-is-installed-using-nvm-but-IntelliJ-doesn-t-know-about-it

If that's the case, there is a solution. Simply copy the two lines, that set path to node using nvm from your `~/.bashrc` 

~~~ bash
export NVM_DIR="/home/_you_/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
~~~

into `~/.profile`.



## flow: polymorphic types and the error: `This type is incompatible with ... some incompatible instantiation of`

Polymorphic types are quite strict: 

> [...] polymorphic types exist to reference the same exact value through a function or class. 
> Not the type of value but the value or a modified version of the value itself.

~ https://github.com/facebook/flow/issues/2194#issuecomment-237899795

## Structure of a npm package, `/src`, `/lib`, `/dist`

The `/src` folder is what the name says. Use your favourite langueage there. 

The `/lib` folder is where your source code will go after transformation (babel). Here the code should be as much compatible/accessible as possible (ES5?). When you `import` this package, npm will use code from `/lib` (because the field `"main": "..."` in`package.json` usualy points to `index.js` in root of the package, but that `index.js` requires files from `/lib`). 

The `/dist` folder is place for your code packed into files ready for users that don't use npm/webpack/...

## `browser` field in `package.json` is for ignoring some files when bundling with webpack

If you want to tell Webpack to ignore some file from your package, you can use the `browser` fiels. Example:

(~ https://github.com/yahoo/intl-messageformat/commit/5082e2919a2672f3408818147aedf6bce1ccba42 ) 

> (...) adds a `"browser"` field to the `package.json` file to hint to
> both Browserify and Webpack that they should _not_ include the data for
> all locales (just English) when bundling for the browser.

package.json

~~~ js
  "browser": {
    "./lib/locales": false,
    "./lib/locales.js": false
  },
~~~

index.js

~~~ js
// Add all locale data to `IntlMessageFormat`. This module will be ignored when
// bundling for the browser with Browserify/Webpack.
require('./lib/locales');
~~~
