[Video link](https://egghead.io/lessons/node-js-add-a-nonce-based-script-src-header-in-express-to-only-allow-scripts-that-match-the-nonce)

# Add a Nonce Based script-src Header in Express to Only Allow Scripts that Match the Nonce

Our site is vulnerable to the remote script injection attack because we are accepting scripts from any https domain.

We could fix this by swapping out our https for code.jquery.com:

```js
app.use(
  helmet.contentSecurityPolicy({
    directives: {
      scriptSrc: ["'self'", "code.jquery.com"],
      reportUri: "/report-violation"
    }
  })
);
```

But now, we'll need to maintain an allow list every time we add a 3rd party script.

There is a better way - using nonces. Let's include the built-in crypto library at the top of our `index.js`.

```js
const crypto = require("crypto");
```

Now, let's add some middleware:

```js
app.use(function(req, res, next) {
  res.locals.nonce = crypto.randomBytes(16).toString("hex");
  next();
});
```

This will add a local variable called nonce which is 16-byte random string called nonce cast to hexadecimal. This is complex and random enough to make it effectively unguessable.

Let's update our CSP now:

```js
app.use(
  helmet.contentSecurityPolicy({
    directives: {
      scriptSrc: ["'self'", (req, res) => `'nonce-${response.locals.nonce}'`],
      reportUri: "/report-violation"
    }
  })
);
```

Then, we can add this value to the end of our jQuery script tag:

```js
`
...
<script src="https://code.jquery.com/jquery-3.4.1.js" nonce="${response.locals.nonce}">
...
`;
```

Now, we can log back into our site and jQuery still loads. We can check our source and see our script tag has a nonce value. This is the same value that is in our CSP attributes.

These two values need to match on every response and request in order for the script to execute. As this particular value of the nonce is replaced on every request cycle we've effectively blocked all remote scripts that we haven't supplied with our nonce.
