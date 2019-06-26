# html-5 

## HTML introduction

The first web browser, Mosaic, was introduced in 1993
there was no "standard" HTML until the introduction of HTML 2.0.

HTML 2.0 was first published in 1995.* HTML 3.0 was published two years later and 4.01 two years after that. HTML 4.01 has been the work horse of the net ever since.

https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5

### Doctype

The doctype for HTML5 is very simple. To indicate that your HTML content uses HTML5, 

```
<!DOCTYPE html>
```

### Sematics in HTML 5
New html elements
```HTML
<section>, 
<article>, 
<nav>, 
<header>, 
<footer> 
<aside>.
```

```HTML
 <mark>
 <figure>
 <figcaption>
 <data>,
 <time>,
 <output>,
 <progress>
 <meter> 
 <main>
```

### HTML audio video tags

Using HTML5 audio and video
The <audio> and <video> elements embed and allow the manipulation of new multimedia content.

```html
new values for the <input> attribute type and the new <output> element.
```

### Form Imporvements
 HTML5 is the ability to validate most user data without relying on scripts. 
`Attributes`
- type [ email, date]
- required [ input box Cannot be empty, if empty cannot submit form]
- pattern [validateing a input field agains regular expressions]
- min and max [ Input field length]
- step attribute [ Incremental value upon clicking arrow in input type number]
- srcdoc and sandbox [ These added as new attributes for iframe to set the level of security of iframe, for more details click https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox[here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox "here") ]
`Psudoclass`
- invalid 
 this will let you apply a specific style to invalid input against the format of the element.
 
 ```html
 <style>
 input:invalid {
    border: 2px solid red;
}
</style>
 <input type="email" value="supportEmail">
 ```
 In the above code if the input does not match email formatting then it will apply invalid style
- 
- valid


### MATH ML
Allowes directly embedding mathematical formula
Currently chrome does not support MATH ML by default, Need a polifill library.
MATH JAX one of the polifill which enables math formulas to be rendererd on browser 
https://www.mathjax.org/#samples


[ In funtoot we use MATHQUIL libarary for MATH ML support ]

### Connectivity 
`Web socket`
The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

In nodeJS `socket.io` is a library which provide web socket accessibility, 





