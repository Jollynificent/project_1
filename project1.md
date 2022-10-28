## Awesome Documentation of lamp stack implementation

#install and update Apache using ubuntu 
`sudo apt update`
`sudo apt install apache2`  

#verify running apache2
`sudo systemctl status apache2`

#check if it can be accessed in the ubutu shell
`curl http:/localhost:80`

#install mysql
`sudo apt install mysql-server -y`

#log into the mysql console
`sudo mysql`
    #insert with "i" the following security script to remove insecure default settings "esc" and ":wq!" to save then exit
"ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';"

#start the interactive script and set password
`sudo mysql_secure_instalation`

#test security and exit the console
`sudo mysql -p`

#install php
`sudo apt install php libache2-mod-php php-mysql`

#confirm php version
`php -v`

#Create the directory
`sudo mkdir /var/www/projectlamp`

#Assign ownership of the directory
`sudo chown -R $USER /var/www/projectlamp.conf`

#Create config file in Apache
`sudo vi /etc/apache2/sites-available/projectlamp.conf`
  #insert with "i" the configuration in the blank file, "esc", and "wq!" to save 
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

#confirm the new file
`sudo ls /etc/apache2/sites-available`

#disable the default website on Apache
`sudo a2dissite 000-default`

#to confirm for syntax errors on config file
`sudo apache2ctl configtest`

#reload Apache to effect changes
`sudo systemctl reload apache2`

#create an index.html file in web root /var/www/projectlamp
`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

#Edit the /etc/apache2/mods-enabled/dir.conf file
`sudo vim /etc/apache2/mods-enabled/dir.conf`

<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
":wq!"

#Reload apache to confirm effected changes
`sudo systemctl reload apache2`

#Create a file in the root folder
`vim /var/www/projectlamp/index.php`

#Insert this line in the file and save with ":wq!"
<?php
phpinfo();

#To remove the file created as it contains sesitive information:
`sudo rm /var/www/projectlamp/index.php`
