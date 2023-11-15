# blog

# Heimdall behind nginx, on Debian 12 - no Docker
As seen in :

https://www.youtube.com/watch?v=e99YQU8rzos

I installed Heimdall v2. in Debian 12:

sudo apt install php-sqlite3 php-bcmath php-json php-xml php-fpm php-mbstring php-gd php-common php-zip
sudo su -
cd /var/www
# download the latest Heimdall release, download links listed here: https://github.com/linuxserver/Heimdall/releases
wget https://github.com/linuxserver/Heimdall/archive/refs/tags/V2.5.8.tar.gz
tar zxvf V2.5.8.tar.gz
mv Heimdall-2.5.8 heimdall
chown -R www-data:www-data heimdall
# If you are proficient in configuring nginx, here is a sample conf that could be put in /etc/nginx/sites-available/heimdall (and then later enabled)...
cd /etc/nginx/sites-enabled
nano ../sites-available/heimdall
