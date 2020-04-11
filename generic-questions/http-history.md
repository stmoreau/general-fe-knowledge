## A brief history of HTTP

- **HTTP 0.9** - Time Berners-Lee released the first documented version of HTTP in 1991.

It consisted of a single line containing a GET method and the path of the requested document. The response was just as simple, returning a single hypertext document without headers or any other metadata.

- **HTTP 1.0** - Version 1.0 received official recognition in 1996, and coincided with the rapid evolution of the HTML specification, and the “web browser.”

The main addition was “request headers” and “response headers.” Also, the new response headers allowed multiple file types, such as HTML, plain text, images, and more.

- **HTTP 1.1** - Version 1.1 was released in 1997 and became the Internet Standard. This version added many performance enhancements, such as keepalive connections, caching mechanisms, request pipelining, transfer encodings, and byte range requests.

This new version was better and removed many of the ambiguities found in HTTP/1.0.

- **HTTP 2.0** - Released in February 2015 by the Internet Engineering Task Force (IETF) focussed on improving the performance of HTTP.

- **HTTP 3** - The new HTTP/3, based on the QUIC protocol, is anticipated to be released in late 2019.

## What is HTTP?

HTTP stands for **Hypertext Transfer Protocol**. It is the foundation of the World Wide Web and is used by browsers to load web pages.

A typical example is when your browser sends an HTTP request to a web server after you enter in an URL. The HTTP command then provides an HTTP response to the web server with the contents of the webpage.

## HTTP Request

HTTP requests typically comprise of the following:

- **Start-line** - This describes the HTTP Method (such as Get, Put, or Post), the request target (such as an URL, or Port), and the HTTP version (such as HTTP/1.1). This start-line is always a single line
- **Request Headers** - An optional set of HTTP headers specifying the request. There are multiple different types of headers:
  - Request Headers - Includes User-Agent, Accept-Type, Accept-Language
  - General Headers - Includes Connection
  - Entity Headers - Includes Content-Type or Content-Length
- **Blank Line** - This confirms that all the request meta-data has been sent
- **Body (Optional)** - This contains all the data associated with the request. There are typically two categories:
  - A body consisting of one single file, defined by the Content-Type and Content-Length Entity Headers
  - A multipart body. One example could be a request containing information in an HTML form

## HTTP Response

HTTP responses typically comprise of the following:

- **Start-line** - This usually includes the HTTP protocol version (HTTP/1.1), a status code (such as 200 or 404), and a textual description of the status code (such as “ok”)
- **Response Headers** - An optional set of HTTP headers specifying the request. There are multiple different types of headers:
  - Response Headers - such as Vary and Accept-Ranges provide more information about the server
  - General Headers - such as Via apply to the whole message
  - Entity Headers - such as Content-Length, or Last-Modified apply to the body of the response
- **Body** - This contains all the data associated with the request. There are typically two categories:
  - A body consisting of one single file, defined by the Content-Type and Content-Length Entity Headers
  - A body consisting of one single resource of unknown length and encoded by chunks (Transfer-Encoding set to Chunked)
  - A multi-part body, with each part containing different information. These are not common

## What is HTTP/2?

HTTP/2 is the next version of HTTP and is based on Google’s SPDY Protocol (originally designed to speed up the serving of web pages). It was released in 2015 by the Internet Engineering Task Force (IETF).

It is important to note that HTTP/2 is not a replacement for HTTP. It is merely an extension, with all the core concepts such as HTTP methods, Status Codes, URIs, and Header Fields remaining the same.

The key differences HTTP/2 has to HTTP/1.x are as follows:

- It is binary, instead of textual
- It is fully multiplexed, instead of ordered and blocking
- It can use one connection for parallelism
- It uses header compression to reduce overhead
- It allows Server Pushing to add responses proactively into the Browser cache

[More information can be found here.](https://www.thewebmaster.com/hosting/2015/dec/14/what-is-http2-and-how-does-it-compare-to-http1-1/)
