# javaScript Lifecycle

https://javascript.info/onload-ondomcontentloaded

## DOMContentLoaded

### State
 the browser fully loaded HTML, and the DOM tree is built, but external resources like pictures <img> and stylesheets may be not yet loaded.

### Event
DOM is ready, so the handler can lookup DOM nodes, initialize the interface.

The `DOMContentLoaded` event happens on the `document` object.

How to catch it
```javascript=
document.addEventListener("DOMContentLoaded", ready);
```
Event gets triggered before loading images
```javascript=
<script>
  function ready() {
    alert('DOM is ready');

    // image is not yet loaded (unless was cached), so the size is 0x0
    alert(`Image size: ${img.offsetWidth}x${img.offsetHeight}`);
  }

  document.addEventListener("DOMContentLoaded", ready);
</script>

<img id="img" src="https://en.js.cx/clipart/train.gif?speed=1&cache=0">

```
### Relation with scripts
While building DOM (document) if the browser encounters a `script` tag inbetween for example`body` it has to load the script and execute the script before it continues including if the scripts are external `(src='')` 

The only exception is `async` and `defer` attributes inside script tags, They basically tell browser to continue processing the without waiting for them to load

#### Async and defer
These attributes will only work if the scripts are external scripts (if there is no `src` tag they are ignored )



|  | Async | Defer |
| -------- | -------- | -------- |
| Order     | Scripts with async execute in the load-first order. Their document order doesn’t matter – which loads first runs first.     | Scripts with defer always execute in the document order (as they go in the document).     |
| DomContentLoaded     | Scripts with async may load and execute while the document has not yet been fully downloaded. That happens if scripts are small or cached, and the document is long enough.     | Scripts with defer execute after the document is loaded and parsed (they wait if needed), right before DOMContentLoaded     |


So async is used for totally independent scripts.

#### Normal Execution
![](https://i.imgur.com/PfAiiDg.png)

#### With Async
![](https://i.imgur.com/7gKch3j.png)

#### With Defer
![](https://i.imgur.com/qUYfIIl.png)

#### Relation with styles
External style sheets don’t affect DOM, and so DOMContentLoaded does not wait for them.

So if we have a script after the style, then that script must wait for the stylesheet to execute:

```javascript=
<link type="text/css" rel="stylesheet" href="style.css">
<script>
  // the script doesn't not execute until the stylesheet is loaded
  alert(getComputedStyle(document.body).marginTop);
</script>
```

#### Built in browser auto fill
https://javascript.info/onload-ondomcontentloaded#built-in-browser-autofill

## load

### State
the browser loaded all resources (images, styles etc).

### Event
additional resources are loaded, we can get image sizes (if not specified in HTML/CSS) etc.


The load event on the window object triggers when the whole page is loaded including styles, images and other resources.

```javascript=
<script>
  window.onload = function() {
    alert('Page loaded');

    // image is loaded at this time
    alert(`Image size: ${img.offsetWidth}x${img.offsetHeight}`);
  };
</script>

<img id="img" src="https://en.js.cx/clipart/train.gif?speed=1&cache=0">
```


## before unload/unload
### State
when the user is leaving the page.

### Event
 the user is leaving: we can check if the user saved the changes and ask him whether he really wants to leave.
 
### window.onunload
When a visitor leaves the page, the unload event triggers on window. We can do something there that doesn’t involve a delay, like closing related popup windows. But we can’t cancel the transition to another page.

For that we should use another event – onbeforeunload.

### window.window.onbeforeunload
If a visitor initiated navigation away from the page or tries to close the window, the `beforeunload` handler asks for additional confirmation.

```javascript=
window.onbeforeunload = function() {
  return "There are unsaved changes. Leave now?";
};
```