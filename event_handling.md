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
* ***Drawback:*** 1 handler per element per event only!

```js
element.onclick = doSomething;
element.onclick = doSomethingElse; // <- overrides previous registration
```


### Microsoft
```js
element.attachEvent('onclick',doSomething)
element.detachEvent('onclick',doSomething)
```
* ***Drawbacks:*** Events always bubble, no way for capturing ???

### W3C

`addEventListener()` (events revolve around this function)
- registers the specified listener on the EventTarget it's called on
- takes three arguments: 
  - **type** (e.g. click)
  - **listener** (function)
  - **useCapture** ???

```js
var button = document.getElementById("createButton");

button.addEventListener("click", function(){ /* ... */ }, false);
```

`removeEventListener()`
- pass the same three arguments mentioned above

```js
var div = document.getElementById("div");

var listener = function(event) { /* ... */ };
div.addEventListener("click", listener, false);
div.removeEventListener("click", listener, false);
```

## jQuery Event Handling



## Event Ordering
## Cancelling Events
## jQuery Event Handling
