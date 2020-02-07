[Video Link](https://egghead.io/lessons/egghead-add-hsts-headers-to-express-apps-to-ensure-all-requests-are-secure)

# 06. Add HSTS Headers to Express Apps to Ensure All Requests are Secure

Taking a belt AND suspenders approach
** In security if there are two ways to mitigate an issues the rest thing to do is implement both **

Right now the browser makes an http request and the server makes the browser to make a second https request

HSTS - HTTP Strict-Transport-Security

Express has a package called Helmet that allows you to add HSTS headers

Add `”helmet”: “^3.21.1”` to the `“dependencies”` in the package.json file.

In index.js add `const helmut = require(“helmet”);`

Then add

```js
app.use(helmet.htsts({
	maxAge: 60 * 60 *24 * 365,
inclueSubdomains: true
preload: true
})
```

HSTS takes a few of parameters `maxAge`  that tells how long HSTS should apply,  and `includeSubdomains`  which tell if all subdomains should be covered or the one were on

Then run `npm i`

Looking at Charles Proxy  you'll see in the headers a 307 status code coming from the browser 
All request after the first will be redirected through https

To protect the first request add the URL to the hstspreload.org directory

## Resources

[HSTS MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)

[307 redirect MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/307)
