# prefecth preconnect and prerender

[article link](https://css-tricks.com/prefetching-preloading-prebrowsing/)

## prefecth

```html
<link rel="prefetch" href="image.png">
```

we're actually requesting and downloading that asset and storing it in the cache. However, this is dependent on a number of conditions, as prefetching can be ignored by the browser. For example, a client might abandon the request of a large font file on a slow network. Firefox will only prefetch resources when "the browser is idle".

### DNS prefetch

This notifies the client that there are assets we'll need later from a specific URL so the browser can resolve the DNS as quickly as possible. Say we need a resource, like an image or an audio file, from the URL example.com. In the `<head>` of the document we'd write:

```html
<link rel="dns-prefetch" href="//example.com">
```

That simple line will tell supportive browsers to start prefetching the DNS for that domain a fraction before it's actually needed. This means that the DNS lookup process will already be underway by the time the browser hits the script element that actually requests the widget. It just gives the browser a small head start.

tiny performance improvement

## Preconnect

Much like the DNS prefetch method, preconnect will resolve the DNS but it will also make the TCP handshake, and optional TLS negotiation. It can be used like this:

```html
<link rel="preconnect" href="https://css-tricks.com">
```

## Prerender

```html
<link rel="prerender" href="https://css-tricks.com">
```

This is like opening the URL in a hidden tab – all the resources are downloaded, the DOM is created, the page is laid out, the CSS is applied, the JavaScript is executed, etc. If the user navigates to the specified href, then the hidden page is swapped into view making it appear to load instantly. Google Search has had this feature for years under the name Instant Pages. Microsoft recently announced they're going to similarly use prerender in Bing on IE11.

When using prerender it's very important to consider the scenarios, Otherwiese the resources will be wasted
