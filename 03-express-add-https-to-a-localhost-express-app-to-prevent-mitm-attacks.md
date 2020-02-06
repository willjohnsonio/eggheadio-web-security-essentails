[Video Link](https://egghead.io/lessons/express-add-https-to-a-localhost-express-app-to-prevent-mitm-attacks)

# 03. add https to a localhost express app to prevent MITM attacks


**http is vulnerable to MITM attacks** 

http passes the session id back and forth to the server with the requests 

Add `”https-localhost”: “^4.4.0”` package in package.json

Then run `npm install`


https-localhost  will replace the express server thats serves over http and server it over https

It enables the protocol and adds a local certificate

In the index.js file `import localHost = require(“https-localhost”)` and change `const port` to `443` instead of 80.

Also we change `const app =localhost(domain)`

Make sure `const domain` is set to `”localhost.charlesproxy”`;

Finally in the console.log make sure it opens to https instead of http

Run `sudo npm start` to restart the server and you will get the lock in the address bar

Now is Charles Proxy it has encrypted data and unknown URLS

## Resources


