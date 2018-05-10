# Flowtype

## React

The types are here: https://github.com/facebook/flow/blob/master/lib/react.js For example the return type of `render()` is `?React$Element<any>`.

## > Error: ... Flow: property `children`. Property not found in props of React element `...`

  This issue is not solved yet. Workaround is to specify `defaultProps` this way:

  ~~~ javascript
class SomeComponent extends React.Component {
	props: {
		children: ?React$Element<any>
	};

	static defaultProps: {
		children: null;
	};
  ~~~

  Changing `propTypes` into flow types in a component that is a `class` means defining the props as an instance field called `props` _inside_ of the class (like above).

## exact type 

`{| |}` defines an exact type

## `required module not found` 

  Maybe the folder `node_modules` is in the ignore section in `.flowconfig`? (Remove it.)
  ~~~
[ignore]
.*/fbjs/.*
.*/node_modules/.*
  ~~~
  
  Or restart flow:
  ~~~
  $> npm run flow -- stop
  $> npm run flow
  ~~~

## optional properties

When two types differs in an optional property, they are no interchangeable, even though they looks almost the same:

~~~ javascript
/* @flow */

type A = {
  s: string,
  n?: number // optional
}

type B = {
 s: string,
 n: number // not optional
}

const a: A = { s: 'AAA' };
const b: B = { s: 'BBB', n: 100 };

// these will cause an error:
const aa: A = b; // b.n can't be undefined, but A allows it 
const bb: B = a; // a.n may be undefined, but B doesn't allow it

// -> types A and B can't be interchanged
~~~

## destructuring

When destructuring an object, adding types this way doesn't work:

  ~~~ javascript
  const { id: number, name: string } = row;
  ~~~

  because that's exactly the way to destructure _into_ a variable with different name than the original field (i.e. here it means initialize the `const number` with the value of `row.id`).
  
  Add the types like this instead:

  ~~~ javascript
  const { id, name }: { id: number, name: string } = row;
  ~~~
  
## flow: polymorphic types and the error: `This type is incompatible with ... some incompatible instantiation of`

Polymorphic types are quite strict: 

> [...] polymorphic types exist to reference the same exact value through a function or class. 
> Not the type of value but the value or a modified version of the value itself.

~ https://github.com/facebook/flow/issues/2194#issuecomment-237899795

## `let` vs `const` in async code

Don't use outside `let` variables inside of an asynchronous code:

~~~ javascript
/* @flow */

const getName = (): ?string => 'Petr';
const loadUser = (name: string): Promise<Object> => Promise.resolve({ name });

const doSomethig = () => {
  let name = getName(); // `name` is of type ?string
  if (name == null) {
    return;
  }
    
  return loadUser(name).then((user) => {
  	if (name.length > 3) {
      //     ^^^^^^ Error, somebody may have changed `name` to null or undefined :(
      // The solution is to define `name` as `const name = ...`.
    }
    // ...
  });
}
~~~

## class implements an interface

When a class implements an interface, there is no `implements` key word. Instead, declare it like this:

~~~ js
interface ISpeak {
  speak(): string;
}

class Person {
  constructor(name) {
    (this: ISpeak)  // <--- HERE
    // ...
  }
  
  speak() {
    // ...
  }
}
~~~
(~ http://stackoverflow.com/a/38224059 )

## cheat sheet

Cheat sheet with many existing types: http://www.saltycrane.com/blog/2016/06/flow-type-cheat-sheet/

## advance features

Advanced features in Flow: http://sitr.us/2015/05/31/advanced-features-in-flow.html

> Flow features prefixed with $ are not technically public, and that the semantics of those features may change

    Table of Contents:
      Class<T>
      $Diff<A,B>
      $Shape<T>
      $Record<T>
      $Supertype<T>
      $Subtype<T>
      $Enum<T>
      Existential types (*)
      Scoped type variables in classes


## type `Object`

Type `Object` can be a _starting point_ for other types. It can be used as any other type. For example this is OK (no flowtype errors):

~~~ js
/* @flow */

type A = {
  getX: () => string
}

function foo(o: Object): A {
  return o; // <-- we can return `o` as type `A` without errors
}
~~~

* When using the `$Keys<T>` type, don't forget to specify the generic type with a constraint `: Object`. So instead of:

  ~~~ js
  function getter<B>(prop: $Keys<B>, b: B) {
    return b[prop];
  }
  ~~~
  
  use:
  
  ~~~ js
  function getter<B: Object>(prop: $Keys<B>, b: B) {
    return b[prop];
  }
  ~~~
  othwerwise flow will complain with an error `access of computed property/element. Computed property/element cannot be accessed on`. 

## stopping flow

To kill all flow processes, use `killall -e flow`.

## type `mixed`

"_mixed is like a safe but somewhat annoying version of any. It should be preferred over any whenever possible._" ( https://flowtype.org/docs/builtins.html#mixed )

~~~ js
/* @flow */
function add(m: number, n: number): number {
  return m + n;
}

function getAny(): any { return 'any'; }
add(getAny(), getAny()); // OK?!

function getMixed(): mixed { return 1; }
add(getMixed(), getMixed()); // ERROR  mixed. This type is incompatible with the expected param type of number

const m = getMixed();
if (typeof m === 'number') {
  add(m, m); // OK
}
~~~

## What type is it?

If you want to know, what type flowtype "see" at some place in your code, use the CLI with argument `type-at-pos`:  

> $ npm run flow -- type-at-pos path/to/file.js 12 34

where `12` is line in file and `34` is position on that line. 

## Union of types is a different type from each of it's types when used as a generic type

~~~ js
/* @flow */

// Type<SomeType> cannot be used as Type<UnionOfSomeTypes>

type New = { type: "NEW" }
type Delete = { type: "DELETE"}

type Action = New | Delete

type Message<A> = { action: A }

function handleMessage(message: Message<Action>) {
  // ...
}



// #1 OK (function returns  Message<Action>)
function createMessageNewAsAction(): Message<Action> {
  return {action: { type: "NEW" }};
}
handleMessage(createMessageNewAsAction())



// #2 ERROR (function returns  Message<New>)
// Cannot call `handleMessage` with `createMessageNew()` bound to `message` 
// because string literal `NEW` [1] is incompatible with string literal `DELETE` [2] 
// in property `type` of type argument `A` [3].
function createMessageNew(): Message<New> {
  return {action: { type: "NEW" }};
}
handleMessage(createMessageNew())
~~~

