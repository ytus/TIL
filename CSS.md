# CSS

## flexbox flex-grow

> (...) rather than telling the browser how wide an element should be, 
> flex-grow determines how the remaining space is distributed 
> amongst the flex items and how big the share is each item receives. 

(~ https://css-tricks.com/flex-grow-is-weird/#article-header-id-2 )

## z-index and stacking context(s)
> (...) z-index only works on positioned elements. If you try to set a z-index on an element with no position specified, 
> it will do nothing

> stacking context confines all of its child elements to a particular place in the stacking order. 
> That means that if an element is contained in a stacking context at the bottom of the stacking order, 
> there is no way to get it to appear in front of another element in a different stacking context that is higher in the stacking order

> New stacking contexts can be formed on an element in one of three ways:
> When an element is the root element of a document (the <html> element)
> When an element has a position value other than static and a z-index value other than auto
? When an element has an opacity value less than 1

(~ https://philipwalton.com/articles/what-no-one-told-you-about-z-index/ )

## sass, `calc()` and variables

If you need to use a variable inside of the `calc` function, do it this way: `height: calc(100% - #{$header-height})`

(~ http://stackoverflow.com/a/20236515 )

## sass, divide a value of a variable with units

You have a variable `$a: 32px` (notuce the unit - `px`) and you need to divide it by two. This `width: #{$a}/2;` will not work (thanks to the unit). Use `calc` like this instead: `width: calc(#{$a}/2);`.

## `overflow` and scrollbars

Scroll bars will be visible:
* `overflow: scroll;` always
* `overflow: auto;` only when necessary

## `box-shadow`

If you set the shadow but can't see it (on one side of the element), give that element some margin so there is actualy enough space around it to show the shadow.

