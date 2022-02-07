#http and https config debian base


- install nginx;
        
        apt install nginx -y
        
- get yours certificates signed as server type and then place;

        .crt file in /etc/ssl/certs
        .key file in /etc/ssl/private
                Note: run chmod 640 .key - to change permissions of .key file
                and run chgrp ssl-cert .key - to change the group of the file (you may need to install ssl-cert)      
        
- now go to /etc/nginx/snippets and cat snakeoil.conf then copy the 2 following lines;

        ssl_certificate /etc/ssl/certs/ssl-cert-snakeoil.pem;
        ssl_certificate_key /etc/ssl/private/ssl-cert-snakeoil.key;

- now cd /etc/nginx/sites-available/;
        
        cp default safe - for example, you can name it what ever you want
        
- then open safe file you just created;

        - delete this 2 lines referents to port 80;
        
                listen 80 default_server;
                listen [::]:80 default_server;        
        
        - then uncomment this 2 lines;
                
                listen 443 ssl default_server;
                listen [::]:443 ssl default_server;

        - paste the 2 lines you cp from snakeoil.conf inside and change .crt and .key to your own;
        
                ssl_certificate /etc/ssl/certs/wwwinova.crt;
                ssl_certificate_key /etc/ssl/private/wwwinova.key;
                
        - and add an s to root /var/www/html; line;
                
                root /var/www/htmls;
                
        - after that save file;
        
- now go to /var/www and create a htmls directory;
        
        cp -r html htmls

- edit your index file as you want;

- now cd /etc/nginx/sites-enabled/ and run;
        
        ln -s /etc/nginx/sites-available/safe safe - to create a soft link for your https config file
        
- after that just restart nginx;

        systemctl restart nginx.service
        
        
        
        



