# How to Request for SSL from Linux Server #

1. Create key and CSR for your Linux system

    a. Execute this query
    
       > $ openssl req -new -newkey rsa:2048 -nodes -keyout test.name.key -out test.name.csr
       
    b .	Fill all required info
    
    c.	Put common name like _*.name.com_ for wild card, _name.com_ for single domain, _test.name.com_ for particular subdomain.

2. Finalize any SSL authority. And use this _.csr_  file to request for SSL certificate.

3. SSL authority will provide you one _.crt_ file and one _.ca-bundle_ file

4. Use _.crt_ and _.key_ file to create _.pfx_ file

     > $ openssl pkcs12 -export -out test.name.pfx -inkey test.name.key -in test.name.crt

# Use .pfx and .ca-bundle file to create HTTPS node server #
     
     var app = new express();
        https.createServer({
                  ca: fs.readFileSync('test_name_com.ca-bundle'), // Provided by SSL authority
                  pfx: fs.readFileSync('test.name.pfx'),
                  passphrase: password // This is that you will use while creation of .key
        }, app).listen(portNo);


