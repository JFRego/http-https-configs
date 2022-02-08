#http and https config red hat based


- first install apache;

        yum install httpd
        
- then install ssl;

        yum install mod_ssl

- next you will create a soft link inside /etc/ssl pointing to /etc/pki/tls/private;

        ln -s /etc/pki/tls/private private
        
- now place your server type signed certificate and key inside;

        .crt file in /etc/ssl/certs
        .key file in /etc/ssl/private

- next you'll need to create a need document root for your https page;

        cp -r /var/www/html /var/www/htmls
        
- now open /etc/httpd/conf.d/ssl.conf;

        - uncomment and replace the document root for your own and edit name server;
                
                <VirtualHost _default_:443>

                # General setup for the virtual host, inherited from global configuration
                DocumentRoot "/var/www/htmls"
                ServerName www.enta.pt:443
                
        - comment this following lines;

                #SSLProtocol all -SSLv3
                #SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA
                
        - then edit cert and key file to your own files;

                SSLCertificateFile /etc/pki/tls/certs/www.enta.crt
                SSLCertificateKeyFile /etc/pki/tls/private/www.enta.key
                
        - after that just save file;

- and thats it, just restart httpd and its done

        systemctl restart httpd             
                
                
