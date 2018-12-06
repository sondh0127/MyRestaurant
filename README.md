# Install requirement environment: LAMP stack
## Apache
`sudo apt update`

`sudo apt install apache2`

## PHP and composer
`sudo apt-get install python-software-properties`
`sudo add-apt-repository ppa:ondrej/php`
`sudo apt-get update`

`sudo apt-get install php7.2 php7.2-xml php7.2-mbstring php7.2-mysql php7.2-json php7.2-curl php7.2-cli php7.2-common php7.2-mcrypt php7.2-gd libapache2-mod-php7.2 php7.2-zip`

`sudo apt-get install curl`
`curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer`

## Mysql and phpmyadmin
`sudo apt-get install mysql-server`
`sudo apt-get install phpmyadmin`

# Go to phpmyadmin and create a database name 'myrest'

# Clone the repository
`cd /var/www/html`

`git clone https://github.com/sonstephendo/MyRestaurant.git`

# Rename folder to: myrest and set permission

`sudo mv /var/www/html/MyRestaurant /var/www/html/myrest`

`sudo chown -R www-data:www-data /var/www/html/myrest/`

`sudo chmod -R 777 /var/www/html/myrest/storage`

# Configure Apache Virtual Host
`sudo gedit /etc/apache2/sites-available/myrest.conf`

```
<VirtualHost *:80>   
  ServerAdmin admin@myrest.test
     DocumentRoot /var/www/html/myrest
     ServerName myrest.test

     <Directory /var/www/html/myrest>
        Options FollowSymLinks
         AllowOverride All
         Order allow,deny
         allow from all
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

# Enable The Laravel And Rewrite Module
`sudo a2enmod rewrite`

`sudo a2ensite myrest.conf`

`sudo service apache2 restart`

# Add server to localhost
`sudo gedit /etc/hosts`

add 
```
127.0.0.1 myrest.test
```
# Restart apache2 sever

`sudo service apache2 restart`

# Clear config
`cd /var/www/html/myrest`

`php artisan config:clear`

# Go to myrest.test