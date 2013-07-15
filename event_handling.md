# JS Event Handling

## Events
  * core of any JS application
  * how JS adds ***interactivity***


## Common Event Types
  * `click`
  * `mousedown`
  * `mouseup`
  * `dblclick`
  * `mousemove`
  * `mouseover` / `mousenter`
  * `mouseout` / `mouseleave`
  * `focus`
  * `blur`
  * `change` (for form inputs)
  * `submit` (for forms)


## Registering Event Handlers to HTML Elements

### inline 
```html
<a href="somewhere.html" onClick="alert('I\'ve been clicked!')">
<a href="somewhere.html" onClick="doSomething()">
```
* ***Don't use it.*** Separate structure/content from behaviour!  


### traditional
```js
//assigning a handler function
element.onclick = doSomething;

//removing a handler function
element.onclick = null;
```
* ***Major drawback:*** 1 handler per element per event only!

### Microsoft


### W3C
 

## Event Ordering
## Cancelling Events
## jQuery Event Handling
