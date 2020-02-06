[Video Link](https://egghead.io/lessons/egghead-simulate-session-hijacking-attacks-and-inspect-network-traffic-with-charles-proxy)

# 02. Simulate Session Hijacking Attacks and Inspect Network Traffic with Charles Proxy

You can use Charles Proxy as a HTTP monitor

Charles Proxy is acting as a Man-In-The-Middle(MITM)

**A MITM is a piece of software usually malicious that sits between the client and the server**

In the filter section  on Charles Proxy type in the URL you’re making a request to and you will have a full list of all the requests that were made and information from those requests.

Click on content>headers to see what was sent it will also show you the cookie that was used with a session id

**Session ID is uniquely generated string that us passed to the server and back in a cookie to identify the users session**

If a hacker has this they can impersonate the user

You can right-click on the url and select copy cURL request

You can paste what was copied in your text editor and modify it

The data parameter in the cURL request shows what is sent as the message. Change it from “message” to “hacked”

Paste the CURL command into the terminal and “HACKED” will display on the page on the users behalf


## Resources

[Mike Sherov MITM Blog Post](https://mike.sherov.com/man-in-the-middle/)
