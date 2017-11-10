# functional programming

## fantasyland

### =>
> equals :: Setoid a => a -> a -> Bool
>
> The => is new notation. What this means is that the signature to its right is valid if all the conditions to its left are satisfied. In the case of equals, the signature a -> a -> Bool is valid if a is a Setoid.

(~ http://www.tomharding.me/2017/03/08/fantas-eel-and-specification-2/ )

### ~>

* The tilde arrow`(~>)` in a type signature is a call of _that_ specific method on an instance of a type. For example here `ap :: Apply f => f a ~> f (a -> b) -> f b` it means calling `ap(...)` on an instance of Apply with an argument of type `f (a -> b)`.
 
 Or:

> equals :: Setoid a => a ~> a -> Bool
>
> The ~> is the new symbol here. What this means is that equals is a method on the thing to the left of ~>, and the thing to the right is its signature.

(~ http://www.tomharding.me/2017/03/08/fantas-eel-and-specification-2/ )


## Maybe is not about null or undefined

Maybe is used to express a missing value, which doesn't neccssarily have to be `null`. `Maybe.nothing()` is not equal `null` and it is possible to create `Maybe.just(null)`. Another thing is thether it's a good idea :-) Probably not.

## `Maybe.map()` vs. `Maybe.chain()`

The function `fun` in `Maybe.map(fun)` shouldn't return `null` or `undefined`. If that's the case, then use `Maybe.chain(fun)` and change the `fun` to return (another) `Maybe`.

## Promise vs. Task (or Future)

_"Promises are inherently stateful & impure, 
but you can hoist the callback pattern into a type similar to a Task 
or Future (variously named in different languages) 
just by storing the binary function that hooks callbacks 
up to some async effect. (...) But this achieves two things that Promises don't: 
it's lazy instead of eager (and hence, pure), 
and it has a synchronously exposed return value."_

~ http://degoes.net/articles/destroy-all-ifs#comment-3137616342

~ https://jsbin.com/guwuqac/edit?js,console

(& https://hackernoon.com/from-callback-to-future-functor-monad-6c86d9c16cb5 )

~~~ js
const Task = (fork) => ({
  fork: fork,
  map: (fn) => Task(
    (reject, resolve) => fork(reject, x => resolve(fn(x)))
  )
})
  
const delayedFive = Task((reject,resolve) => setTimeout(resolve,400,5))
const logError = (e) => console.log('error=', e);
const logOutput = (out) => console.log('out=' + out)

delayedFive
  .map((i) => i * 2)
  .map((i) => i + 3)
  .fork(logError, logOutput); // -> "out=13"
~~~

## debugging a functional code with Ramda
Try `R.tap((x) => console.log('x=', x))` from [ramda](http://ramdajs.com/docs/#tap).

_"Runs the given function with the supplied object, then returns the object."_


## monads

> Monads express how computations in the context of a particular type are chained together. 

> [Monads are] confusing elements of imperative code be[ing] encapsulated into explicit types [which] makes debugging and unit testing way easier.

(~ https://www.quora.com/Is-there-an-example-use-of-Monads-which-is-clearly-better-than-closures-with-mutable-state )

> The trick of pure fundamentalist functional languages is to have obsessive-compulsive types and expose all effects explicitly in the type signatures using monads, distinguishing between the types of pure values and the types of computations on values that may entail effects.

> Once effects are explicit in, say, the I/O monad, operations such as allocating mutable variables, and reading and writing to them, must be lifted into the I/O monad.

> The real power of monads comes from the fact that computations are themselves just values that can be passed around as first-class citizens within the pure host language.

(~ https://queue.acm.org/detail.cfm?id=2611829 )

### Reader

>  Represents a computation, which can read values from a shared environment, pass values from function to function, and execute sub-computations in a modified environment.

(~ https://hackage.haskell.org/package/mtl-2.2.1/docs/Control-Monad-Reader.html )

> (...) often a function cannot be pure. For example, it may need to access some global information just for reading. We could just add another parameter to the function:
>
>     readerFunc :: GlobalConfig -> Int -> Int
>
> But it is often easier to use a monad, since they are easier to compose.
>
>     readerFunc2 :: Int -> Reader GlobalConfig Int

(~ https://stackoverflow.com/a/18911314 )

> Yet another way of saying the same thing: 
> `Reader r a` is something that consumes `r` and produces `a`, and the Functor, Applicative and Monad instances are basic patterns for working with Readers. 
> * Functor = make a Reader that modifies the output of another Reader 
> * Applicative = connect two Readers to the same input and combine their outputs 
> * Monad = inspect the result of a Reader and use it to construct another Reader. 
> * The `local` and `withReader` functions = make a Reader that modifies the input to another Reader.

(~ https://stackoverflow.com/a/14206724 )

### Writer

#### `lister` and `pass`

> It's now clear that `listen` gives you access to the log produced by a Writer action inside the Writer monad, and `pass` gives you a way to alter the log inside the Writer monad.

(~ https://stackoverflow.com/a/34834078 )

### State

### RWS

In theory, Reader, Writer and State monads can be replaced by a functions with more input parameters or a function that returns more than one value. But:

> The haskell one not only tells us the types needed for parameters and the return type, but also what the function may affect. For example, it can't do any IO, nor can it read or change any global state, or access any static configuration data. Neither may be true for the c# function, but we cannot tell.

> (...) consider a function which:
> * Needs to read from a ProgramConfig data type
> * Write values to a string for logging
> * Use and modify a ProgramState value.
>
> We could do something like this:
>
>     data ProgramData = ProgramData { pState :: ProgramState, pConfig :: ProgramConfig, pLogs :: String } complexFunction :: Int -> State ProgramData Int
>
> However, that type isn't very accurate. It implies that the ProgramConfig may be changed, which it won't. It also implies that the function may use the pLogs value, which it won't. Also, testing it is more complex, as theoretically, the function could accidently change the program config, or use the current pLogs value in its computations.
>
> This can be greatly improved upon with this:
>
>     betterFunction :: Int -> RWS ProgramConfig String ProgramState Int
>
> This type is very accurate. We know that the ProgramConfig is only ever read from. We know the String is only ever changed. The only part that requires both reading and writing is the ProgramState, as expected. This is easier to test, as we only need to test different combinations of ProgramConfig, ProgramState and Int for input, and check the output Int, String and ProgramState for output.

(~ https://stackoverflow.com/a/18911314 )

## `bind` is `map`, `collapse`, monad is `bind` and `create`

> Monads are just a set two or three operations on a data structure, which obey certain laws. 
> The operations are either (`map(function,structure)`, `collapse(structure)`, `create(value)`) or  (`bind(function,structure)`, `create(value)` ) where you can implement map and collapse in terms of bind, and vice versa. 
> map(function,structure) is a function that applies a function to every element in the structure. Pretty straightforward. For example:

    -> map(addThree,[1,2,3])
    [4,5,6]

> Collapse is a function which takes structures embedded in a structure of the same type, and gets rid of one level.

    -> collapse([[],[3,4],[6,1,2]])
    [3,4,6,1,2]

> Create takes a value and puts it into the structure in the simplest way possible.

    -> create(3)
    [3]

> These three functions are enough to have a monad over your structure

(~ https://news.ycombinator.com/item?id=6349837 )

## articles

* [Functors, Applicatives, And Monads In Pictures](http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html)
* [Three Useful Monads](http://adit.io/posts/2013-06-10-three-useful-monads.html)
* [Lenses In Pictures](http://adit.io/posts/2013-07-22-lenses-in-pictures.html)
* [Fantas, Eel, and Specification 1 - ?](http://www.tomharding.me/2017/03/03/fantas-eel-and-specification/)
* [Practical Intro to Monads in JavaScript: Either](https://tech.evojam.com/2016/03/21/practical-intro-to-monads-in-javascript-either/)

## books

* [Functional-Light JavaScript](https://github.com/getify/Functional-Light-JS) (from getify)
* [Functional Programming in JavaScript
](https://www.manning.com/books/functional-programming-in-javascript#downloads)
* [Mostly adequate guide](https://drboolean.gitbooks.io/mostly-adequate-guide/content/)

## lists

* [Awesome FP JS](https://github.com/stoeffel/awesome-fp-js#lenses)

## videos

* [Professor Frisby Introduces Composable Functional JavaScript](https://egghead.io/lessons/javascript-linear-data-flow-with-container-style-types-box)

## ???

* [monet.js - Powerful abstractions for JavaScript: All monads](https://cwmyers.github.io/monet.js/#all-monads)
