# functional programming

## Maybe is not about null or undefined

Maybe is used to express a missing value, which doesn't neccssarily have to be `null`. `Maybe.nothing()` is not equal `null` and it is possible to create `Maybe.just(null)`. Another thing is thether it's a good idea :-) Probably not.

## monads



### Reader

> (...) often a function cannot be pure. For example, it may need to access some global information just for reading. We could just add another parameter to the function:
>
>     readerFunc :: GlobalConfig -> Int -> Int
>
> But it is often easier to use a monad, since they are easier to compose.
>
>     readerFunc2 :: Int -> Reader GlobalConfig Int

(~ https://stackoverflow.com/a/18911314 )

### Writer

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
