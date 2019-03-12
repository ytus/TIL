## 📄
* [realworld](https://github.com/gothinkster/realworld) The mother of all demo apps

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


## Structure of a npm package, `/src`, `/lib`, `/dist`

The `/src` folder is what the name says. Use your favourite langueage there. 

The `/lib` folder is where your source code will go after transformation (babel). Here the code should be as much compatible/accessible as possible (ES5?). When you `import` this package, npm will use code from `/lib` (because the field `"main": "..."` in`package.json` usualy points to `index.js` in root of the package, but that `index.js` requires files from `/lib`). 

The `/dist` folder is place for your code packed into files ready for users that don't use npm/webpack/...

### Scripts in ./node_modules/.bin
Those scripts can be run directly without `npm`, for example: 

    $> npm install source-map-explorer
    $> ./node_modules/.bin/source-map-explorer dist/bundle.js dist/bundle.js.map 

And this will not (and should not!) work:

    $> npm run source-map-explorer 
    $> npm ERR! missing script: source-map-explorer

~ https://github.com/npm/npm/issues/10413#issuecomment-230542256


## `browser` field in `package.json` is for ignoring some files when bundling with webpack

If you want to tell Webpack to ignore a file that is in your package, you can use the `browser` field. 

Spec: https://github.com/defunctzombie/package-browser-field-spec

Example: 

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

## moment.js

### How to create a moment only with date without time

Use `.startOf('day')`. 

(~ https://stackoverflow.com/a/19699447) 

### How to set UTC offset when construncting a moment instance

Calling `utcOffset(...)` changes the time of the current moment. Use the second parameter (boolean) to prevent it: 

> The utcOffset function has an optional second parameter which accepts a boolean value 
> indicating whether to keep the existing time of day.
> One use of this feature is if you want to construct a moment 
> with a specific time zone offset using only numeric input values

(~ https://jsbin.com/xajurup/edit?js,console )
(~ http://momentjs.com/docs/#/manipulating/utc-offset/ )

## redux-loop (+ promise + catch)

* When creating an `Effect.promise(functionThatReturnsPromise)`, the promise returned from `functionThatReturnsPromise` should resolve with an action. But don't forget to add a `catch()` handler to that promise and it should return an action too! (Of course, most likely it will be some other action.)

## ESLint
* The rules `no-unused-vars` allows to define a pattern, that it will ignore. For example to ignore names that start with an undescore: 
~~~ javascript
  'no-unused-vars': ['error', {
    vars: 'local', varsIgnorePattern: '^_',
    args: 'after-used', argsIgnorePattern: '^_' }],
~~~

## `Array.reduce` doesn't need the initial value

_"If `initialValue` is provided in the call to reduce, 
then `accumulator` will be equal to `initialValue` and `currentValue` will be equal to the first value in the array. 
If no `initialValue` was provided, then accumulator will be equal to the first value in the array 
and `currentValue` will be equal to the second."_

~ http://devdocs.io/javascript/global_objects/array/reduce

## Object destructuring and default values

It's possible to use destructuring to retrieve a value from a hierarchy of objects even if some part of it is missing: 

~~~ js
const present = {
  first: {
    second: {
      third: {
        value: 'something'
      }
    }
  }
};

const missing = {
  // no `first`
};

const {first: {second: {third: {value: v1}}}={}} = present;
console.log('v1=', v1); // -> "v1=" "something"

const {first: {second: {third: {value: v2}={}}={}}={}} = missing;
console.log('v2=', v2); // -> "v2=" undefined (and no errors!)
~~~

## parameters with default values doesn’t count on the length property of a function

_"Using default assignments wherever it makes sense can help you write more self-documenting code._

_(...)_

_There’s a caveat here: parameters with default values doesn’t count on the length property of a function. This may be useful to know if you’re doing some kind of meta-programming with the length property"_

~ https://medium.com/@sminutoli/theres-a-caveat-here-parameters-with-default-values-doesn-t-count-on-the-length-property-of-a-e7433f8adcce#.fkqll7g1x

~~~ js
> var createKey = function (a, b, c) { return `${a}:${b}:${c}`; }
< undefined
> createKey.length
< 3
> var createKey2 = function (a, b='_', c='_') { return `${a}:${b}:${c}`; } // Two default values here.
< undefined
> createKey2.length
< 1
~~~ 

## `onClick`, `event.target` vs. `event.currentTarget` and event bubbling vs capturing

Events in HTML can be caught bubbling (going inside out) or captured (going outside in). If you want to do `capture` in React, use `onClickCapture` instead of `onClick`. The `event.target` contains the element where the event started bubbling up. The `event.currentTarget` is the element where the event was first captured going in. They are both DOM nodes (`DOMEventTarget` type in React/flowtype). 

You can get the value of an attribute from DOM node like this: 

    const key = event.currentTarget.attributes.getNamedItem('data-key').value;

~ http://javascript.info/tutorial/bubbling-and-capturing

~ https://facebook.github.io/react/docs/events.html#mouse-events

~ http://stackoverflow.com/questions/20377837/how-to-access-custom-attributes-from-event-object-in-react#comment66849996_31706457

## Static method of a class

Two different ways to define a static method on a class, _both compile OK_, but only the second works:

~~~ js
class A {
  static f = f;
}
const f = () => console.log('f');
A.f(); // -> error: A.f is not a function
~~~

~~~ js
const f = () => console.log('f');
class A {
  static f = f;
}
A.f(); -> 'f'
~~~
