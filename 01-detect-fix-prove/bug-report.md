# Bug Report — as reported by the app's own error-reporting SDK

**Project:** testbed (a minimal Express app built specifically to validate
this pipeline — see the top-level README for why)

**Error message:**
```
TypeError: Cannot read properties of undefined (reading 'toUpperCase')
```

**File:** `app.js`, line 25

**Severity:** high (assigned automatically)

**Stack trace, exactly as reported:**
```
TypeError: Cannot read properties of undefined (reading 'toUpperCase')
    at /app/app.js:25:37
    at Layer.handle [as handle_request] (/app/node_modules/express/lib/router/layer.js:95:5)
    at next (/app/node_modules/express/lib/router/route.js:149:13)
    at Route.dispatch (/app/node_modules/express/lib/router/route.js:119:3)
    at Layer.handle [as handle_request] (/app/node_modules/express/lib/router/layer.js:95:5)
    at /app/node_modules/express/lib/router/index.js:284:15
    at router.process_params (/app/node_modules/express/lib/router/index.js:346:12)
    at next (/app/node_modules/express/lib/router/index.js:280:10)
    at expressInit (/app/node_modules/express/lib/middleware/init.js:40:5)
    at Layer.handle [as handle_request] (/app/node_modules/express/lib/router/layer.js:95:5)
```

**What actually happened:** a GET request to `/api/greet` with no `?name=`
query parameter reached this line in the original code:

```js
app.get('/api/greet', (req, res) => {
  const name = req.query.name;
  const greeting = 'Hello, ' + name.toUpperCase() + '!';
  res.json({ greeting });
});
```

`req.query.name` is `undefined` when the parameter is omitted, so
`.toUpperCase()` throws.

**Root cause, as diagnosed automatically:** the value being read was never
checked for existence or type before it was used.
