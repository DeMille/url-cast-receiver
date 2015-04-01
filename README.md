# URL Cast Receiver

**Custom chromecast receiver to display webpages without tab casting**

Try it with the [sender demo](https://demille.github.io/url-cast-receiver).

## Usage

You can use a hosted version now (use **ASFDF333** for your appId),
or you can clone / customize this repo and host your own.

URLs are sent to the receiver by sending messages on the `urn:x-cast:com.url.cast` namespace.

There are two ways to cast a URL to the reciever, each with pros and cons:

**Method 1:** Loading the URL in an iframe
- Pros: Reciever stays intact after loading page
- Cons: `X-Frame-Options: SAMEORIGIN` errors

```js
// iframe method
var namespace = 'urn:x-cast:com.url.cast';
var msg = {
    "type": "iframe",
    "url": "http://example.com"
}

session.sendMessage(namespace, msg, onSuccess, onErr);
// reciever is still alive
```

**Method 2:** Changing the window location on the chromecast
- Pros: Can load any URL, no iframe origin issues
- Cons: Reciever gets overridden with page load, so you can no longer communicate with it without stopping the cast and restarting.

```js
// iframe method
var namespace = 'urn:x-cast:com.url.cast';
var msg = {
    "type": "loc",
    "url": "http://example.com"
}

session.sendMessage(namespace, msg, onSuccess, onErr);
// receiver is now basically dead to you
```

## Notes

- The chromecast renders webpages at a viewport size of 1280x720 instead of 1080x1920 like you might expect, so be prepared for that.

- The default background color on the chromecast is black, so pages loaded with method 2 (the window location) might have a surprise black background.  If you use the iframe method, the receiver sets the body to white.

## License

The MIT License (MIT)

Copyright (c) 2015 Sterling DeMille &lt;sterlingdemille@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.