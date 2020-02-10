[Video link](https://egghead.io/lessons/egghead-add-a-default-src-csp-header-in-express-to-enforce-an-allowlist-and-mitigate-xss)

# Add a default-src CSP Header in Express to Enforce an Allowlist and Mitigate XSS

We can use our CSP to be able to mitigate against the iFrame style attack from the last lesson.

```js
app.use(
  helmet.contentSecurityPolicy({
    directives: {
      defaultSrc: ["'none'"],
      scriptSrc: ["'self'", (req, res) => `'nonce-${response.locals.nonce}'`],
      reportUri: "/report-violation"
    }
  })
);
```

Setting the defaultSrc property to `none` will stop any iFrames from being opened.

We now need to extract our CSP from scriptSrc to a variable and explicitly define the same CSP for a number of other Srcs.

```js
const selfNonceSrc = [
  "'self'",
  (req, res) => `'nonce-${response.locals.nonce}'`
];
app.use(
  helmet.contentSecurityPolicy({
    directives: {
      defaultSrc: ["'none'"],
      scriptSrc: selfNonceSrc,
      imgSrc: selfNonceSrc,
      connectSrc: selfNonceSrc,
      styleSrc: selfNonceSrc,
      reportUri: "/report-violation"
    }
  })
);
```

This means we allow scripts, images, XHR and styles from ourselves but from no-one else. We do not allow anything else.

If we log in to our site now and try our iFrame attack we can see that this will not be successful.

We have now mitigated against inline scripts, remote scripts and iFrame attacks.
