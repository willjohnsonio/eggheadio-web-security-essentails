[Video Link](https://egghead.io/lessons/egghead-redirect-all-http-traffic-to-https-in-express-to-ensure-all-responses-are-secure)

# 04. Redirect All HTTP Traffic to HTTPS in Express to Ensure All Responses are Secure


If we remove the `https://`  from the URL in the address bar it will say the site cannot be reached 

A redirect is needed

In index.js under `app.listen(port):`

Add 
```js
const redirApp = express();
redirApp.use(function(req, res) {
	Return res.redirect(`https://${domain}${eq.url}`
});
redirApp.listen(80);
```

Now if a request comes in on post 80 it will redirect to https

This change exposes the cookie though wil fix in next lesson

## Resources
