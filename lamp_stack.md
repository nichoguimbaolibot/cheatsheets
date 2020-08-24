# Setup E-commerce Application

```bash
#install a firewall
sudo yum install firewalld
sudo service firewalld start #start the firewall service
sudo systemctl enable firewalld #run in boot up

#install a mariadb
sudo yum install mariadb-server
sudo vi /etc/my.cnf #configure the file with the right port `my.conf` is the default configuration file for mysql and mariadb
sudo service mariadb start # start mariadb service
sudo systemctl enable mariadb # run mariadb in boot up
sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp #enable firewall to the 3306 port
sudo firewall-cmd --reload  #reload the firewall to load the latest changes

mysql
CREATE DATABASE ecomdb;
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
FLUSH PRIVILEGES;
#load data
mysql < db-load-script.sql

sudo yum install -y httpd php php-mysql
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp #enable port 80 for the httpd
sudo firewall-cmd --reload  #reload the firewall to load the latest changes

sudo vi /etc/httpd/conf/httpd.conf #Configure DirectoryIndex to use index.php instead of index.html

sudo service httpd start
sudo systemctl enable httpd

sudo yum install -y git
git clone ${repo_url}.git /var/www/html

#Test the app
curl http://localhost

```