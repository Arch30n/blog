# blog

# Heilmdall install on debian 12 / nginx
As seen in :

https://www.youtube.com/watch?v=e99YQU8rzos

I installed Heimdall v2. in Debian 12:

sudo apt install php-sqlite3 php-bcmath php-json php-xml php-fpm php-mbstring php-gd php-common php-zip
download the latest Heimdall release, as listed here: https://github.com/linuxserver/Heimdall/releases
tar zxvf v2.4.13.tar.gz
cd Heimdall-2.4.13/
php artisan serve --host=192.168.x.y --port=8080
