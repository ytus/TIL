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

(~ https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)
