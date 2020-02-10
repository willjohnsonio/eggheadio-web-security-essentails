[Video link](https://egghead.io/lessons/egghead-make-an-xss-payload-to-read-document-body-from-a-vulnerable-website)

# Make an XSS Payload to Read document.body from a Vulnerable Website

We've stopped a specific XSS attack but we haven't mitigated the danger in general.

We can see that there are other payloads we can send, including sensitive user information. Our attacker could use something like `document.body.innerText` as a payload which would send a request to our malicious site with the sensitive information.
