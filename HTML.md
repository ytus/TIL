# HTML

## onhover vs. onmouseover

There is no `onhover` attribute in HTML, it's called `onmouseover`. And it's all lowercase (but if you declare it in JSX, use `onMouseOver`). 

## Which element has currently focus?

> document.activeElement

~ https://stackoverflow.com/a/497108/337483

## `onkeydown` on a `div`

The `div` needs a `tabindex` attribute for `onkeydown` handler to work. `tabindex=0` (no speficic order) is enough.

(~ http://stackoverflow.com/a/3149416)

