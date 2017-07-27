# React

## Event's `stopPropagation()` doesn't work

When you attach a listener to an element _outside_ of React e.g.:

~~~ js
document.addEventListener("keydown", (e: KeyboardEvent) => ... )
~~~

and then try to stop React's synthetic event in a React's event handler:

~~~ js
_handleKeyDown = (e: SyntheticKeyboardEvent) => {
  if (...) {
    ...  
    e.stopPropagation();
  }
}
~~~

the event will be still propagated into the first event handler (but there it would be a _native_ browser's event, not a React's synthetic event). You have to use `e.nativeEvent.stopImmediatePropagation();` instead: 

~~~ js
_handleKeyDown = (e: SyntheticKeyboardEvent) => {
  if (...) {
    ...  
    e.nativeEvent.stopImmediatePropagation();
  }
}
~~~

* https://medium.com/@ericclemmons/react-event-preventdefault-78c28c950e46
* https://stackoverflow.com/a/24421834
