
## Nginx Overview

1. High performance
2. High Concurrency
3. Low resource usage

## Nginx vs Apache

* apache is configures in pre fork mode which means that had spawned a set number of processors.
* Niginx deals with requests asynchrnously
* nignx can serve static resources much faster than apache

## To install nginx

```
sudo apt-get install nginx
```
### to enable firewall

```
sudo ufw enable
```
### To check nginx version

```
nginx -v
```

### To check the available nginx applications 

```
sudo ufw app list
```
### To allow port 80 and port 443

```
sudo ufw allow 'Nginx Full'
```

### To ckeck the nginx status

```
sudo systemctl status nginx
```

### install developmental tools
```
current directory ./configure
sudo apt-get instal build-essential
sudo apt-get install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev             // required packages for ubuntu
yum install pcre pcre-deve1 zlib zlib-devel openssl openssl-devel   // required packages for centos
```

### nginx options
```
nginx -h

Usage: nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/share/nginx/)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file
```

