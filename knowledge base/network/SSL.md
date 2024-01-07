

If server A calls server B, then server B's certificate should be either

- in A's keystore
- signed by a CA certificate that is in A's keystore
- signed by an intermediate certificate that is signed by a CA certificate that is in A's keystore. If you do this then server B must also provide the intermediate certificate during negotiation.
- as above with more and more intermediate certificates.

I assume we are talking about communication between your own machines, and not client browsers you don't control.

If you have hundreds of machines you may find some advantages to using an intermediate certificate, if not just distribute your own CA certificate to your keystores. This lets you change certificates without having to modify the keystores on all the clients.

As for your second question, if you really want to use ssl between your reverse proxy and your WL back-end, look at [Apache ProxyPassReverse and https](https://serverfault.com/questions/33072/apache-proxypassreverse-and-https) for general syntax and [https://httpd.apache.org/docs/current/mod/mod_ssl.html#SSLProxyCACertificateFile](https://httpd.apache.org/docs/current/mod/mod_ssl.html#SSLProxyCACertificateFile) for specifying the CAs that the proxy will consider from its upstream.


https://serverfault.com/questions/762197/ssl-certificate-installation-to-establish-ssl-connectivity-between-2-servers