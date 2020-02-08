[Video Link](https://egghead.io/lessons/egghead-add-csrf-token-middleware-to-an-express-server-to-mitigate-csrf)

# 09. Add CSRF Token Middleware to an Express Server to Mitigate CSRF


In package.json add `”csurf: “^1.10.0”`in the dependencies then `npm install`

In index.js add  `const csurf = require(“csurf”)`

Then add new middleware `app.use(csurf());`

In the input.js file add  `<input type=”hidden” name=”_csrf” value=${request.csrfToken()}>`

When this form is submitted `csrf()` will be passed as a value 

`.value_csrf` will be compared to the random number we attach to the users session. If the value match success

If they don’t match add

 ```js
app.use function(err, req, res, next)) {
	If (err.code !== EBADCSRFTOKEN“) return next(err);

res.status(403).send(“csrf detected”)
})
```
We need to place the same `csfr` token from login.js (`<input type=”hidden” name=”_csrf” value=${request.csrfToken()}>`)

Place it in message.js

On the `<button>` add `data -csrftoken=${request.csrftoken()}`

In the index.js file in our static folder in the `headers:` key add `”csrftoken” : e.target.dataset.csrftoken,` as the value

## Resources
