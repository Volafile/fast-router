node.js fast-router
===================

A fast & simple O(log n) URL router for node.js that can be used for almost
anything.

Runtime: O(log n), where *n* is the total number of routes. The runtime is O(n) if you consider *n* the length of your longest route.

Usage:
-----

```js
//Require the module...
var Router = require("fast-router").Router;
//Create a new router
var router = new Router();
```

That's all. Now you can begin to add routes:

```js
router.addRoute("/", rootNode);
router.addRoute("/users/:user/:thing", someValue); 
//Keys are used and indicated by ':' . They will capture that part in the URL.
router.addRoute("/static/*", someOtherValue); 
//A wildcard is indicated by a '*' and will capture the rest of the URL
router.addRoute("/static/robots.txt", specialMagic); 
//Exact matches always take precendence over wildcards and paths with keys
```

To match some URL against the route tree:

```js
var result = router.parse("/users/tim/lamp");
var result = router.parse("/static/main/js/local/script.js");
var result = router.parse("/");
```


Result
------

A result is a javascript object with the following properties:

```js
{
    url: <url>,
    //contains the URL as parsed with node.js's built-in url.parse(_url, true)
    value: <value>,
    //The value that was supplied when the route was inserted. You could use
    //a function for it to emulate the behavior of some other routers.
    parts: [...],
    //The parts of the URL as the result of url.pathname.split('/')
    keys: {key: value, ...},
    //The keys used in the URL with their respective values, 
    //for the first example this would be {user: "tim", thing: "lamp"}
    extra: "<etc>/<etc>/<etc>..."
    //The text matched by the wildcard if the route contained one
}
```
