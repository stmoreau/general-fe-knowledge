# What happens when you type in a URL?

“What happens when you type in a URL” is a deceptive question commonly asked in tech interviews. If you look online, there are many [very detailed resources](https://github.com/alex/what-happens-when) but few concise explanations of how a web browser, a server, and the general internet work together.

This is how I would explain it:

1. You enter a URL into a web browser
2. The browser looks up the IP address for the domain name via DNS
3. The browser sends a HTTP request to the server
4. The server sends back a HTTP response
5. The browser begins rendering the HTML
6. The browser sends requests for additional objects embedded in HTML (images, css, JavaScript) and repeats steps 3-5
7. Once the page is loaded, the browser sends further async requests as needed
