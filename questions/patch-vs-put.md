# Main Difference Between PUT and PATCH Requests

The main difference between PUT and PATCH requests are in the way the server processes the enclosed entity to modify the resource identified by the Request-URI.

In a PUT request, the enclosed entity is considered to be a modified version of the resource stored on the origin server, and the client is requesting that the stored version be replaced.

With PATCH, however, the enclosed entity contains a set of instructions describing how a resource currently residing on the origin server should be modified to produce a new version.

Also, another difference is that when you want to update a resource with PUT request, you have to send the full payload as the request whereas with PATCH, you only send the parameters which you want to update.

Suppose we have a resource that holds the first name and last name of a person.

If we want to change the first name then we send a put request for Update

```js
{ "first": "Michael", "last": "Angelo" }
```

Here, although we are only changing the first name, with PUT request we have to send both parameters first and last.
In other words, it is mandatory to send all values again, the full payload.

When we send a PATCH request, however, we only send the data which we want to update. In other words, we only send the first name to update, no need to send the last name.

For this reason, PATCH request requires less bandwidth.
