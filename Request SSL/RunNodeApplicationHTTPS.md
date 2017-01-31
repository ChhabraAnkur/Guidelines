# How to Request for SSL from Linux Server #

1. Create key and CSR for your Linux system
    a. Execute this query
  * > openssl req -new -newkey rsa:2048 -nodes -keyout test.name.key -out test.name.csr
    b.	Fill all required info
    c.	Put common name like *.name.com for wild card, name.com for single domain, test.name.com for particular subdomain.

2. Finalize any SSL authority. And use this .csr  file to request for SSL certificate.

3. SSL authority will provide you one .crt file and one .ca-bundle file

4. Use .crt and .key file to create .pfx file 
    * > openssl pkcs12 -export -out test.name.pfx -inkey test.name.key -in test.name.crt


