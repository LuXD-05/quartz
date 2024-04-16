---
public: true
edited_seconds: 1450
modified_at: 16/04/2024 19:25:02
---
### What's a cookie?
A **cookie** is an info that a website puts on a user's pc. They store limited info about a browsing session on a website that can be retrieved in the future. They can be accessed by the browser, a website o by a 3rd party; and common use cases include: session management, personalization and tracking. They appeared for the 1st time on the Netscape browser to help it understand if a user had already visited a website.
### Types
There are many types of cookies:
- **HTTP cookies**: an <u>overall category</u> of cookies used with modern web browsers to enable specific capabilities.
- **Session cookies**: cookies which <u>persist while the user is browsing</u> or visiting a website and till its session expires.
- **Persistent cookies**: (a.k.a. <u>permanent cookies</u>), they <u>persist</u> for a configurable <u>duration of time</u> or <u>until a certain date</u> (both set by the web server).
- **1st-party cookies**: (a.k.a. <u>SameSite cookies</u>), them and the info they contain is <u>restricted to the same site</u> on which they were set.
- **3rd-party cookies**: cookies which <u>enable entities other than the original site to access them</u> for user tracking and personalization purposes.
- **Zombie cookies**: cookies that <u>persist even after attempting to delete them</u>.
- **Flash cookies**: these are a <u>specific type of cookie</u> (neither HTTP nor browser cookies) that decline in the use of ***Flash*** (now no longer widely used).
- **Secure cookies**: <u>1st</u> and <u>3rd party</u> cookies that can only be sent over <u>encrypted HTTPS connections</u>.
### Are they safe?
##### Privacy
Cookies are <u>generally safe</u>, but **3rd-party cookies** are sometimes seen as **intrusive** and considered a form of **spyware**. By allowing **3rd-party entities** to <u>track users' behavior in a way that they might not even be aware of</u>, they may **violate the users' privacy**. An example is constituted by **advertisers** that use cookies to provide **targeted ads**. To protect users' privacy, 3rd-party cookies are subject to the **GDPR**.
##### Security
Threat actors can also **hijack 3rd-party cookies** in order to <u>gain access to the user's info</u> and enable them to <u>launch other attacks</u> (such as: ***session hijacking*** and ***cross-site scripting***).
**Unsecured cookies** (cookies transmitted <u>unencrypted over HTTP</u>) are also a problem that has **risks**: if a cookie contains **sensitive data** (like login or financial info) and is sent **unencrypted**, upon **interception** it could be used by a criminal. However, to mitigate this risk, it's sufficient to <u>secure the cookie</u> enabling it to be transmitted only over **HTTPS**. 