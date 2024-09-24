**SSTI** (Server-Side Template Injection) is a type of vulnerability that occurs when user input is embedded unsafely within server-side templates. This can lead to the execution of arbitrary code on the server. Many web applications use templating engines to dynamically generate HTML pages. If user input is directly included in the template without proper validation or escaping, an attacker may inject malicious code into the template, leading to code execution.

## Example of How SSTI Works

Suppose you have a web application that uses a templating engine like Jinja2 in Python. If user input is directly included in the template, such as:

```java
template = "{{ user_input }}"
output = Template(template).render(user_input="<script>alert(1)</script>")
```


An attacker might be able to inject code like `{{ 7*7 }}`. In a vulnerable system, this would evaluate to 49 on the server side, demonstrating that the server is evaluating the user input as code.