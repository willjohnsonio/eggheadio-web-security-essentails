[Video Link](https://egghead.io/lessons/egghead-web-security-course-overview)

# 01. Web Security Course Overview

**These instructions are for macOS**

* Download Charles Proxy [charlesproxy.com/download](https://www.charlesproxy.com/download)
* Download Git run `git --version` in the command line to check if you have it [git](https://git-scm.com/downloads)
* Download Node.js run `node --version` make sure you have a version higher than 8.9.3 [nodejs](https://nodejs.org/en)
* Download npm ot comes with node, check the version `npm --version`
* Download curl check the version with `curl --version` if you don't have curl go to [curl.haxx.se](https://curl.haxx.se)

Make sure you have `sudo` privileges

Open and change the hosts file

```bash
code /etc/hosts
```
At the `127.0.01 localhost` line add evil.com and save it.

```
127.0.01 localhost evil.com
```

Run `sudo npm install` from the root of the repo

Then `cd exercises/01` then run `sudo npm start`

Visit the http://localhost.charlesproxy.com url there should be a username and password prompt

Run `sudo npm run start:evil.com` then will start a new server at https://evil.com:666/index.html.
