[Video link](https://egghead.io/lessons/egghead-prepare-a-vulnerable-website-for-csp-enforcement-with-report-only-csp-headers-in-express)

# Prepare a Vulnerable Website for CSP Enforcement with Report Only CSP Headers in Express

To protect our site against XSS, we need to validate and encode user input. This is a big task and can often be overlooked which is why XSS is a big problem in the wild.

There is an additional way to protect against this type of attack called CSP or Content Security Policy. This allows us to define the type of resources that are allowed to load and where to report violations.

```js
app.use(
  helmet.contentSecurityPolicy({
    directives: {
      scriptSrc: ["'self'", "https:"],
      reportUri: "/report-violation"
    },
    reportOnly: true
  })
);
```

We are doing a few things here:

- First, we are telling express only to execute scripts from our own domain and, because we are importing jQuery over https, also over https.
- Next, we are giving an endpoint where the server can report violations.
- Finally, because we don't yet know if this policy will stop our app from working properly, we are running in reportOnly mode. This will cause violations to be reported but will still run the violating scripts.

```js
app.route("/report-violate").post((req, res) => {
  console.log("CSP Violation: ", req.body || "No data received");
  res.status(200).send("ok");
});
```

This sets up the endpoint that the CSP can post to and logs any violations to the server.

The reports posted by express are JSON formed and are of MIME type application/csp-report. This means we need to add a body parser to our application. Let's install and import a body parser.

On the command line,

```bash
npm install body-parser --save
```

At the top of our `index.js` file:

```js
const bodyParser = require("body-parser");
```

And then, in our app we need to parse the JSON when the MIME type is of "application/csp-report".

```js
app.use(
  bodyParser.json({
    type: ["json", "application/csp-report"]
  })
);
```

Now, once we've restarted our server and tried our attack again we'll see that even though it is successful there is also a request to `report-violation` as we have configured it.

Once this has been in production for a while, we can remove reportOnly mode.

If we try now to post our malicious code, then no request is made to our evil.com domain. This effectively mitigates XSS script injection.
