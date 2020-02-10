[Video link](https://egghead.io/lessons/egghead-set-the-httponly-cookie-flag-in-express-to-ensure-cookies-are-inaccessible-from-javascript)

# Set the httpOnly Cookie Flag in Express to Ensure Cookies are Inaccessible from JavaScript

We know that the site is vulnerable to XSS and that can be used to steal `document.cookie`. Let's fix that specific problem - in later lessons we'll see how to protect against XSS in general.

By default, when a cookie is set it can be accessed by `document.cookie` or it is sent in every request to the target domain. If we inspect the cookie, we can see it doesn't set the httpOnly flag.

In the `index.js` file, where the session cookie settings are saved. The httpOnly property is set to false. If we remove this property, save, clear the cookies and reload, we'll see that the httpOnly flag is set.

```js
...

app.use(
  session({
    secret: "key",
    resave: false,
    saveUninitialized: true,
    cookie: {
      sameSite: "lax",
      secure: true,
      httpOnly: false
    }
  })
);

...
```

Now, if we log back in and send our malicious payload again, we'll see that the message succeeds but it does not contain our cookie value.

So, if you don't need access in your application to the `document.cookie` value, set this httpOnly flag when setting cookies.
