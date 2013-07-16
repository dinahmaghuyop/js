# JS Event Handling

## Events
  * core of any JS application
  * adds ***interactivity***


## Common Event Types
  * `click`
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
element.onclick = doSomething;
element.onclick = null;
```
* ***Drawback:*** 1 handler per element per event only!


### Microsoft
```js
element.attachEvent('onclick',doSomething)
element.detachEvent('onclick',doSomething)
```
* ***Drawback:*** Events always bubble, no way for capturing ???

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


## The Event Model
* `target` - Element to which the event was originally dispatched
* `currentTarget` - Element whose EventListeners are currently being processed. This is particularly useful during capturing and bubbling. 
* `type` - Name of the event



## Event Ordering
If an element and one of its ancestors have an event handler for the same event type, 
which one should fire first when the event is triggered? http://jsfiddle.net/uYQkc/12/


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
$button.addEventListener("click", function(){ /* ... */ }, true);
```

Example:

```js
$parentDiv.addEventListener('click', doSomething1, true);
$childDiv.addEventListener('click', doSomething2, false);
```



## Canceling Events

### event.preventDefault
Default action of the event will not be triggered


### event.stopPropagation
Prevents further propagation, 
preventing any parent handlers from being notified of the event


### event.stopImmediatePropagation
* Preventing any further handlers from being called at all—even if they’re on the same element
* Prevents further propagation



## jQuery Event Handling
http://jsfiddle.net/q7bT4/2/      
DOM Tree: https://docs.google.com/a/clinic-it.com/drawings/d/1-ChklbNhDLgH8GfRJxsfSdgmKw5z2b1vNfQQqAtzKRg/edit
###`on()` - `off()`
mostly syntax sugar that can mimic `bind()`, `live()`, or `delegate()` depending on how you call it

 * `bind()` - `unbind()`
   - assigns handler to EACH matched element -> costly!   
   - dynamically added elements won't get the handler
 
 ```js
 $("#members li a").on("click", function(e){}); 
 
 $("#members li a").bind("click", function(e){}); 
 $("#members li a").click(function(e){}); 
 ```
  
 * `live()` - `die()`
   - assigns handler to document, propagates to matched element
   - deprecated  
 
 ```js
 $(document).on("click", "#members li a", function(e){}); 

 $("#members li a").live("click", function(e){});
 ```
 
 * `delegate()` - `undelegate()`
   - assigns handler to specific element, propagates to matched element
   - great for dynamically added elements 

 ```js
 $("#members").on("click", "li a", function(e){}); 
 
 $("#members").delegate("li a", "click", function(e){});
 ```
 
###`trigger()`
   - execute all handlers and behaviors attached to the matched elements for the given event type
   - custom events
   - event continues to propagate through its ancestors
   - http://jsfiddle.net/cKSQc/1/

 ```js
 var $parent = $('#parent'),
     $child = $('#child');
 
 $parent.on('custom', function(e){ 
     alert('Parent Custom Event');
 });
 
 
 $parent.on('click', function(e){
     $parent.trigger('custom');
 });
 ```
 
###`triggerHandler()`
   - trigger handlers bound via jQuery without also triggering the native event
   - does not propagate
 
 ```js
 var $parent = $('#parent'),
     $link = $('#link');

 $link.on('click', function(e){
     e.preventDefault();
     alert('Link');
 });
 
 
 $parent.on('click', function(e){
     $link.triggerHandler('click');
 });
 ```


## Sources:
* Javascript Web Applications - Alex MacCaw
* https://developer.mozilla.org/en-US/docs/Web/API/Event
* http://www.quirksmode.org/js
* http://api.jquery.com/category/events/
* http://www.elijahmanor.com/2012/02/differences-between-jquery-bind-vs-live.html
* http://www.alfajango.com/blog/the-difference-between-jquerys-bind-live-and-delegate/

