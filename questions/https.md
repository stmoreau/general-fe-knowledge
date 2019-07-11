# What Is HTTPS, and Why Should I Care?

HTTPS, the lock icon in the address bar, an encrypted website connection—it’s known as many things. While it was once reserved primarily for passwords and other sensitive data, the entire web is gradually leaving HTTP behind and switching to HTTPS.

The “S” in HTTPS stands for “Secure”. It’s the secure version of the standard “hypertext transfer protocol” your web browser uses when communicating with websites.

## How HTTP Puts You At Risk

When you connect to a website with regular HTTP, your browser looks up the IP address that corresponds to the website, connects to that IP address, and assumes it’s connected to the correct web server. Data is sent over the connection in clear text. An eavesdropper on a Wi-Fi network, your internet service provider, or government intelligence agencies like the NSA can see the web pages you’re visiting and the data you’re transferring back and forth.

There are big problems with this. For one thing, there’s no way to verify you’re connected to the correct website. Maybe you think you accessed your bank’s website, but you’re on a compromised network that’s redirecting you to an impostor website. Passwords and credit card numbers should never be sent over an HTTP connection, or an eavesdropper could easily steal them.

**These problems occur because HTTP connections are not encrypted**. HTTPS connections are.

## How HTTPS Encryption Protects You

HTTPS is much more secure than HTTP. When you connect to an HTTPS-secured server—secure sites like your bank’s will automatically redirect you to HTTPS—your web browser checks the website’s security certificate and verifies it was issued by a legitimate certificate authority. This helps you ensure that, if you see “https://bank.com” in your web browser’s address bar, you’re actually connected to your bank’s real website. The company that issued the security certificate vouches for them. Unfortunately, certificate authorities sometimes issue bad certificates and the system breaks down. Although it isn’t perfect, though, HTTPS is still much more secure than HTTP.

When you send sensitive information over an HTTPS connection, no one can eavesdrop on it in transit. HTTPS is what makes secure online banking and shopping possible.

It also provides additional privacy for normal web browsing, too. For example, Google’s search engine now defaults to HTTPS connections. This means that people can’t see what you’re searching for on Google.com. The same goes for Wikipedia and other sites. Previously, anyone on the same Wi-Fi network would be able to see your searches, as would your Internet service provider.

## How Does HTTPS Work?

HTTPS is based on one of two types of Encryption Protocol, either **Secure Sockets Layer** (SSL) or **Transport Layer Security** (TLS). Many websites will use an SSL Certificate to encrypt the communication.

Both TLS and SSL use an Asymmetric Public Key Infrastructure whereby a ‘public’ key and a ‘private’ key are used to encrypt the data.

The private key is stored on the web server whereas the public key is, as it’s name suggests, in the public domain and is used to decrypt encrypted data sent from the web server and vice versa.

When your browser initiates an HTTPS session with the web server, the server sends the public key to your browser and an ‘SSL Handshake’ is then performed between the browser and the server. Once the secure connection is initiated and accepted the browser recognises the secure link and shows the link as secure either with a green browser bar or padlock, depending on the type of SSL certificate being used.

## What Are The Benefits Of HTTPS?

- **More Trust** – HTTPS reassures potential customers that you are a secure and responsible business
- **More Transparency** – Prospective customers can see that you are a genuine business and you own the domain name
- **Improved Conversion Rates** – Customers are far more likely to complete a purchase if they see that your site is secured
- **More Traffic** – HTTPS is a stated Google Ranking Factor so business using HTTPS can get a better ranking than less secure competitors
