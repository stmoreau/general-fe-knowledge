# JWT

JSON Web Token (JWT) is a JSON-based open standard for creating access tokens that assert some number of claims, JWT is just a string with the following format:

```
header.payload.signature
```

### Header:

The header identifies which algorithm is used to generate the signature, there are basically two main algorithms that we use HS256 and RS256.

```
{
"alg" : "HS256",
"typ" : "JWT"
}
```

alg - The type of algorithm we will use to sign the token.

typ - Define the type of the token which is JWT.

### Payload:

Payload contains our claims that we want to store (personal data that we define) and some standard claims.

```
{
"Name" : "Moshe Binieli",
"Email" : "mmoshikoo@gmail.com"
}
```

As we said there are also some standard claims for example:

- iat: Time when the token is issued by us.
- exp: The expiration time of the token.

### Signature:

Signature step is pretty simple, in this step we take the header and payload and convert it to Base64 format.
The formatted strings are concat with ‘.’ between them and we get something like xxxxx.yyyyy

```
data = base64urlEncode(header) + "." + base64urlEncode(payload)
```

Then we take the new string we’ve just created and we use hash algorithm and hash it with the chosen secret key.

```
hashedData = hashAlgorithm(data, secretKey)
```

Finally we convert the signature string to Bas64 as well and we’re done.

```
signature = base64urlEncode(hashedData)
```

![jwt-example](jwt.png)

## How this is actually works in real life?

Let’s take a classic case of login, the client sends a Username and Password, when the information arrives at the server we authenticate the user against the database. Let’s suppose we want to keep the user ID and role in the claims in our token.

We take the required information and create an object that looks like this:

```
{
"ID" : 123,
"Role" : "Admin"
}
```

Then we define our header properties ”alg” and “typ” as object.
We convert our header and the payload (ID, Role) to Base64.

We concat those strings into one string separated by dot, header.payload.
Then we hash the data and convert the signature to Base64 as I explained in signature part.

We concat those strings into one string separated by dot, header.payload.
Then we hash the data and convert the signature to Base64 as I explained in signature part.
