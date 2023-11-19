# blog

## Heimdall behind nginx, on Debian 12 - no Docker

- **Install php** 
```
sudo apt install php-sqlite3 php-bcmath php-json php-xml php-fpm php-mbstring php-gd php-common php-zip
```
- **Download the latest Heimdall release, download links listed here: https://github.com/linuxserver/Heimdall/releases**
```
sudo su -
cd /var/www
wget https://github.com/linuxserver/Heimdall/archive/refs/tags/v2.5.6.tar.gz
tar zxvf v2.5.6.tar.gz
mv Heimdall-2.5.6 heimdall
chown -R www-data:www-data heimdall (or nginx:nginx)
```
- **Configuring nginx, here is a sample conf that could be put in /etc/nginx/sites-available/heimdall (and then later enabled)**

Edit the nginx config file
```
cd /etc/nginx/sites-enabled
nano ../sites-available/heimdall.conf
```
Paste into heimdall.conf the following code :
```
server {
    listen 443 ssl;
    http2 on;

    ssl_certificate     /etc/letsencrypt/live/arch30n.ddns.net/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/arch30n.ddns.net/privkey.pem; # managed by Certbot
#    ssl_certificate     /etc/nginx/ssl/pveproxy-ssl.pem;
#    ssl_certificate_key /etc/nginx/ssl/pveproxy-ssl.key;

#    ssl_stapling on;
#    ssl_stapling_verify on;

#    server_name arch30n.ddns.net localhost;
    server_name _;

    root /var/www/heimdall/public/;
    client_max_body_size 5M;
    index index.php index.html;
    location / {
        # needed by PHP Laravel, or /users, /items, /tags, /settings don't work
        try_files $uri $uri/ /index.php?$query_string;
    }
    # serve static files directly
    location ~* ^.+\.(jpg|jpeg|gif|png|ico)$ {
       access_log off;
    }
    # pass PHP scripts on Nginx to FastCGI (PHP-FPM) server
    location ~ \.php$ {
       include snippets/fastcgi-php.conf;
       fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    }
}
```

Edit fpm autorizations : 
```
nano /etc/php/7.4/fpm/pool.d/www.conf to change user and group:

listen.owner = nginx or www-data
listen.group = nginx or www-data
;listen.mode = 0660
```
