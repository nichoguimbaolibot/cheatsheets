# Apache Web Server

```bash
nicho1125:~  yum install httpd

service httpd start

service httpd status

firewall-cmd --permanent --ad-service=http #if you have a firewall configuration enable this will enable the http traffic

cat /var/log/httpd/acces_log # view success access logs

cat /var/log/httpd/error_log #view error logs

#Config file location

cat /etc/httpd/conf/httpd.conf #you can configure the port, the document root, servername, etc.
Listen 80 #Port of apache web server
DocumentRoot "/var/www/html" #where your static file is hosted
ServerName www.houses.com:80 #dns name

#This is the configuration to set web servers
<VirtualHost *:80>
    ServerName www.houses.com
    DocumentRoot /var/www/houses
</VirtualHost>

<VirtualHost *:80>
    ServerName www.oranges.com
    DocumentRoot /var/www/oranges
</VirtualHost>

#any changes on httpd.conf needs to restart run this command
service httpd restart

#you can external import the setup for virtual host by creating a .conf file
#/etc/httpd/conf/houses.conf
<VirtualHost *:80>
    ServerName www.houses.com
    DocumentRoot /var/www/houses
</VirtualHost>
#/etc/httpd/conf/oranges.conf
<VirtualHost *:80>
    ServerName www.oranges.com
    DocumentRoot /var/www/oranges
</VirtualHost>

Include conf/houses.conf
Include conf/oranges.conf

```

# Install Apache Tomcat

```bash
yum install java-1.8.0-openjdk-devel

wget https://downloads.apache.org/tomcat/tomcat-8/v8.5.53/bin/apache-tomcat-8.5.53.tar.gz

tar xvf apache-tomcat-8.5.53.tar.gz

./apache-tomcat-8.5.53/bin/startup.sh

#Apache Tomcat Directory
ls -l apache-tomcat-8.5.53

```
