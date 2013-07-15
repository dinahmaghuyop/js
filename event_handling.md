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

* `addEventListener()` (events revolve around this function)
  * registers the specified listener on the EventTarget it's called on
  * takes three arguments: 
     - **type** (e.g. click)
     - **listener** (function)
     - **useCapture** ???

```js
var button = document.getElementById("createButton");

button.addEventListener("click", function(){ /* ... */ }, false);
```

* `removeEventListener()`
  - pass the same three arguments mentioned above

```js
var div = document.getElementById("div");

var listener = function(event) { /* ... */ };
div.addEventListener("click", listener, false);
div.removeEventListener("click", listener, false);
```

## jQuery Event Handling
* `bind()` - `unbind()`
  - assigns handler to EACH matched element 
  - costly!
* `live()` - `die()`
  - assigns handler to document, propagates to matched element
  - depracated
* `delegate()` - `undelegate()`
* `on()` - `off()` 



## The Event Model
* `target` - Element to which the event was originally dispatched
* `currentTarget` - Element whose EventListeners are currently being processed. This is particularly useful during capturing and bubbling. 
* `type` - Name of the event



## Event Ordering
If an element and one of its ancestors have an event handler for the same event type, 
which one should fire first when the event is triggered? http://jsfiddle.net/uYQkc/8/


```html
<div id="super-parent">
    <div id="parent">
        <div id="child">Hello</div>
    </div>
</div>
```


###Capturing
Triggers event listeners from the top-most ancestor to the element in question
(i.e. from the outside in)


###Bubbling
Triggers event listeners from the element, propagating up through its ancestors
(i.e. from the inside out)


###W3C Model
Events are first captured until they reach the target element; then, they bubble up again.


This is where the `useCapture` argument of `addEventListener()` comes into picture
* `true`  :  event handler is set for the capturing phase
* `false` :  event handler is set for the bubbling phase

```javascript
// Use capturing by passing true as the last argument
button.addEventListener("click", function(){ /* ... */ }, true);
```



## Canceling Events

### event.preventDefault
Default action of the event will not be triggered


### event.stopPropagation
Prevents the event from bubbling up the DOM tree, 
preventing any parent handlers from being notified of the event


### event.stopImmediatePropagation
* Preventing any further handlers from being called at all—even if they’re on the same element
* Prevents the event from bubbling up the DOM tree


## Sources:
* Javascript Web Applications - Alex MacCaw
* https://developer.mozilla.org/en-US/docs/Web/API/Event
* http://www.quirksmode.org/js
* http://api.jquery.com/category/events/

