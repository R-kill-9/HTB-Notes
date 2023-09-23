Cross-Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker injects malicious code, usually in the form of scripts, into a web page or application, which is then executed by unsuspecting users who visit that page. The injected code can steal sensitive data, manipulate web content, or perform actions on behalf of the user without their consent.

There are three main types of XSS attacks:

1. **Stored XSS:** The malicious code is permanently stored on a server and is served to multiple users when they access a specific page or resource. This type of XSS can have a long-lasting impact as it affects all subsequent visitors to the compromised page.
    
2. **Reflected XSS:** In this case, the injected code is reflected off a web server and immediately executed in response to a user's request. Typically, the attacker tricks the user into clicking on a malicious link containing the payload.
    
3. **DOM-based XSS:** This type of XSS occurs when the client-side script in a web page manipulates the Document Object Model (DOM) without proper sanitization or validation, allowing an attacker to execute malicious code on the client-side.
### Basic script
```bash
<script>alert("hi")</script>
```

### Image script
With this type of script we are trying to upload an image, but providing a wrong source. We generate this error on purpose to execute the *onerror* javascript function that prints hi in a pop-upp suing alert.
```bash
<img src='x' onerror=alrt("hi") />
```

Also, we can use the onclick javascript's function. If we upload an image with a valid source when we click the image it will spawn the pop-up with the alert message.
```bash
<img src"<valid url>" onclick=alert("hi") />
```