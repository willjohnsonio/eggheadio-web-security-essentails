[Video Link](https://egghead.io/lessons/egghead-mitigate-csrf-attacks-by-setting-the-samesite-cookie-flag-in-express)

# 08. Mitigate CSRF Attacks by Setting the SameSite Cookie Flag in Express

The session id is still exposed even from the attackers website

**The sameSite cookie property determines whether the cookie is allowed to be sent cross site or not**

It defaults to a value of `none` which allows cross site

You can set it to `lax` as long as the request is GET and a top level navigation then cookies will be sent

You can also set it to `strict` this will log you out when clicking go back

**Chrome 80 will now default to lax**




## Resources

[OWASP SameSite](https://www.owasp.org/index.php/SameSite)
