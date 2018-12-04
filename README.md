# Install requirement environment: LAMP stack

`sudo apt update`

`sudo apt install apache2`

`sudo apt install php7.2 libapache2-mod-php7.2 php7.2-mbstring php7.2-xmlrpc php7.2-soap php7.2-gd php7.2-xml php7.2-cli php7.2-zip`

`curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer`


# Clone the repository
`cd /var/www/html`

`git clone https://github.com/sonstephendo/MyRestaurant.git`

# Rename folder to: myrest

`sudo mv /var/www/html/myrest`

`sudo chown -R www-data:www-data /var/www/html/myrest/`

`sudo chmod -R 775 /var/www/html/myrest/`

# Configure Apache2
`sudo nano /etc/apache2/sites-available/myrest.conf`

```language
<VirtualHost *:80>   
  ServerAdmin admin@example.com
     DocumentRoot /var/www/html/myrest/
     ServerName myrest.test

     <Directory /var/www/html/myrest/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

# Enable The Laravel And Rewrite Module
`sudo a2ensite myrest.conf`

`sudo a2enmod rewrite`

`sudo systemctl restart apache2.service`

# Add server to localhost
`sudo nano /etc/hosts`

add 
```
127.0.0.1 myrest.test
```
restart apache2 sever

`sudo service apache2 restart`