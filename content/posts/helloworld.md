---
title: "Helloworld"
date: 2017-09-02T18:25:00+08:00
draft: true
---

Chiba grenade 3D-printed face forwards render-farm network soul-delay cartel warehouse. Dead marketing plastic Chiba motion sunglasses voodoo god neural carbon concrete dolphin rain footage beef noodles. Geodesic skyscraper jeans soul-delay kanji wristwatch sensory. Car receding construct paranoid spook sign silent artisanal hacker knife j-pop plastic city corrupted. Bridge plastic motion Kowloon advert weathered tattoo car crypto-augmented reality pen rain. Network franchise dome stimulate apophenia futurity augmented reality tube boat human concrete into plastic beef noodles. 

## Custom shortcodes

[https://gohugo.io/templates/shortcode-templates/](https://gohugo.io/templates/shortcode-templates/)

## Vimeo example

{{< vimeo id="146022717" class="vimeo-wrapper" >}}


## Code example

{{< figure src="/img/example.jpg" title="example" >}}

{{< gist spf13 7896402 >}}

{{< instagram BYTAI7ildek hidecaption >}}

{{< highlight bash >}}

# As root
## Set up non-root user
adduser caddyuser
usermod -aG sudo caddyuser

## Login as non-root user
su - caddyuser

## Set up SSH
ssh-keygen -t rsa -b 4096
# Copy local machine ssh pubkey to /home/caddyuser
cat localmachine_pubkey.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
sudo systemctl reload sshd

## Init UFW (firewall)
# List available app rules
sudo ufw app list

sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status # Should display OpenSSH as allowed

## Install MySQL
sudo apt-get install mysql-server
sudo mysql_secure_installation
# Test MySQL
systemctl status mysql.service
## Outputs
# ● mysql.service - MySQL Community Server
#    Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
#    Active: active (running) since Sun 2017-08-20 14:47:37 UTC; 2min 18s ago
#  Main PID: 13767 (mysqld)
#    CGroup: /system.slice/mysql.service
#            └─13767 /usr/sbin/mysqld

## Configure MySQL
# Log into MySQL
mysql -u root -p
# In MySQL
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
# Set username and password. Must use later when setting up WP
GRANT ALL ON wordpress.* TO '<wordpressuser>'@'<localhost>' IDENTIFIED BY '<password>';
# Flush privileges to notify the MySQL server of the changes
FLUSH PRIVILEGES;
EXIT;

## Install PHP7 (min. req. for WP 4.8.1)
sudo apt-get install php7.0-fpm php7.0-mysql php7.0-curl php7.0-gd php7.0-mbstring php7.0-mcrypt php7.0-xml php7.0-xmlrpc

## Install Caddy
curl -s https://getcaddy.com | bash

# Set up Caddy directories
sudo mkdir /etc/caddy
sudo chown -R root:www-data /etc/caddy
sudo touch /etc/caddy/Caddyfile
sudo mkdir /etc/ssl/caddy
sudo chown -R www-data:root /etc/ssl/caddy
sudo chmod 0770 /etc/ssl/caddy
sudo mkdir /var/www
sudo chown www-data:www-data /var/www

# Install Caddy as a system service
sudo curl -s https://raw.githubusercontent.com/mholt/caddy/master/dist/init/linux-systemd/caddy.service -o /etc/systemd/system/caddy.service
sudo systemctl daemon-reload
# Start Caddy on boot
sudo systemctl enable caddy.service
sudo systemctl status caddy.service

## Add UFW (firewall) rules for HTTP and HTTPS access
sudo ufw allow http
sudo ufw allow https

# Init Caddyfile
sudo vim /etc/caddy/Caddyfile

###### Insert the following text ######
http:// { # use domain name when ready to do SSL/TLS
  root /var/www
  gzip
  # tls caddyuser@example.com ## add this line when ready to add SSL/TLS
}

# Start Caddy
sudo systemctl start caddy

## Download WP
wget https://wordpress.org/latest.tar.gz
tar -xvf latest.tar.gz && rm latest.tar.gz
sudo mv wordpress /var/www/wp
sudo chown -R www-data:www-data /var/www/wp


## Caddyfile for WP
example.com {
    tls admin@example.com
    root /var/www/wordpress
    gzip
    fastcgi / /run/php/php7.0-fpm.sock php
    rewrite {
        if {path} not_match ^\/wp-admin
        to {path} {path}/ /index.php?_url={uri}
    }
}


{{< /highlight >}}

[example ref]({{< ref "posts/linkeg.md" >}})
[example relref]({{< relref "posts/linkeg.md#header2" >}})
