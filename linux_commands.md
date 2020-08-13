# User Accounts

```bash
foo@bar:~$ whoami #To know the current user

foo@bar:~$ id #To know the id

foo@bar:~$ su ${username} #To switch user
```


# Download Files

```bash
foo@bar:~$ wget ${url_of_file} -O ${new_file_name} #To download a file and save it locally
foo@bar:~$ curl wget ${url_of_file} -O

foo@bar:~$ ls /etc/*release* #To check OS version

foo@bar:~$ cat /etc/*release* #To know more information of the OS
```

# Redhat Package Manager
```bash
rpm -i ${package_name_location} #to install a package

rpm -e ${package_name_location} #to uninstall a package

rpm -q ${package_name_location} #to get package information or query
```

# Yum

```bash
yum install ${package_name} #install a package

yum repolist #to list all available repositories

yum install ${url_of_packge}

yum list ${package_name} #to know the information of the installed package

yum list #to see all of the installed packages

yum remove ${package_name} #to remove a package or uninstall

yum --showduplicates list ${package_name} #to show duplicated packages

ls /etc/yum.repos.d/ #file where the repositories are configured

cat /etc/yum.respos.d/${repo_name} #you can see the url where the repo are stored
```

# Services

```bash
services httpd start #(or systemctl start ${service_name}) To start HTTPD service

systemctl stop ${service_name} #to stop a service

systemctl status ${service_name} #to check status of service

systemctl enable ${service_name} #configure to start the service at startup

systemctl disable ${service_name} #configure to not start at startup

#${location_of_the_service} ${location_of_the_code}
/usr/bin/python3 /opt/code/my_app.py #this will start a simple python web server this can be use to other serivces
curl http://localhost:5000 #returns "Hello World"

#to start an application without specificying the location of the service and the code you can use the "/etc/systemd/system"
# where you will create a file with a .service extension
# example: my_app.service and inside the my_app.service this is the content
# [Service]
# ExecStart=/usr/bin/python3 /opt/code/my_app.py
# after you edit and save run this command
# systemctl daemon-reload #to reload to know that there is a new service configured
# after that you can run the my_app.service
# systemctl start my_app
# if you want to configure the application to run on bootup you can add an additional section which is the [Install]

# [Service]
# ExecStart=/usr/bin/python3 /opt/code/my_app.py
# [Install]
# WantedBy=multi-user.target #the app will run after the multi-user.target application

#then you can run `systemctl enable my_app`

#if your application has to run an application before it starts you can add a ExecStartPre and ExecStartPost
# [Unit]
# Description=My python web application
#
# [Service]
# ExecStart=/usr/bin/python3 /opt/code/my_app.py
# ExecStartPre=/opt/code/configure_db.sh
# ExecStartPost=/opt/code/email_status.sh
#
# [Install]
# WantedBy=multi-user.target #the app will run after the multi-user.target application

# service unit file Docker
# /lib/systemd/system/docker.service
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
BindsTo=containerd.service
After=network-online.target firewalld.service containerd.service
Wants=network-online-target
Requires=docker.socket

[Service]
Type=notify
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
ExecReload=/bin/kill -s HUP $MAINPID
Restart=always
StartLimitBurst=3
StartLimitInterval=60s
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity

[Install]
WantedBy=multi-user.target
```

# IP Address

```bash

ip addr show #show all available ip address

# lo is for loopback and eth0 is for connectivity

# if there is no ip address for connectivity is set you can set it
# by usign this command:

ip addr add 192.168.1.10/24 dev eth0

```

# Search

```bash
# -i edit files in place (makes backup if SUFFIX supplied)
# sudo sed -i 's/${value}/${replace_value}' ${filename}
sudo sed -i 's/8080/9090/g' file.txt
```


