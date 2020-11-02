PANTEON
--------

Panteon is a one-page site with interactive elements in simple CSS. Panteon is simple and therefore can always be improved by adding JS and connecting libraries. Panteon will tell you about the flight to Mars and, perhaps, help you fulfill your dream of flying to it! (Just by filling out the form)

Instructions for linux server
--------
1. Install nginx

```bash
sudo apt update
sudo apt-get install nginx
```
2. Go to the directory 
```bash
cd /var/www/html/
```  
  Clone the repository
```bash
clone https://github.com/hideto13/panteon.git
```
3. Create a directory
```bash
sudo mkdir /etc/nginx/ssl/
cd /etc/nginx/ssl/
```
4. Generate a certificate

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout localhost.key \
-out localhost.crt
```
5. Answering questions, example

```
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:New York
Locality Name (eg, city) []:New York
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Home
Organizational Unit Name (eg, section) []:IT
Common Name (e.g. server FQDN or YOUR name) []:localhost
Email Address []:no-reply@localhost
```
6. Change configurations in the default file

```bash
vim /etc/nginx/sites-available/default
```
```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        listen 443 ssl;

        ssl on;
        ssl_certificate /etc/nginx/ssl/localhost.crt;
        ssl_certificate_key /etc/nginx/ssl/localhost.key;
        root /var/www/html/panteon/;

        index index.html index.htm index.nginx-debian.html;

        server_name ip.adress;

        location / {
                try_files $uri $uri/ =404;
        }
```
7. Restart nginx
```bash
sudo service nginx restart
```
8. This site is now available for viewing at:

```
https://ip.adress
```
