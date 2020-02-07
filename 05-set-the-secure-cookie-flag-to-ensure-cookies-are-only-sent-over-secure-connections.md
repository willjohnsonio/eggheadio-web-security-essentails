[Video Link](https://egghead.io/lessons/egghead-set-the-secure-cookie-flag-to-ensure-cookies-are-only-sent-over-secure-connections)

# 05. Set the Secure Cookie Flag to Ensure Cookies are Only Sent Over Secure Connections

**There is a property of cookies called secure**  

Passing `secure` when we set or cookies it will only send https

In the index.js file go to app.use and  on `cookie`  add `secure: true’

This will add secure to the cookie command




## Resources

[OWASP Secure Cookie Flag Docs](https://owasp.org/www-community/controls/SecureFlag)
