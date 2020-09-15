
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

## configuration terms

* Directive - A specific config options that get set in the config files and consist of a name and a value
```
server_name mydomain.com;
```
* Context - Sections within the configuration where diectives can be set for that given context.
    * contexts are like scope
    * They inherit from their parrent

![nginx](img/context.png?raw=true "Title")

### define a virtual host

* each virtual hots being a new server context or server block like so a virtual host or server context is essentially responsible for listening on a port typically port 80 for http or port 443 for https for a given ip address or a domain.
```
events {}

http {
    include mime.types;

    server {
        listen 80;
        server_name 52.66.247.22;

        root /data/www;
    }
}
```
### location blocks

```
events {}

http {
    include mime.types;

    server {
        listen 80;
        server_name 52.66.247.22;

        root /data/www;
    }

    ## prefix match
    location /greet {
        return 200 'hello from NGINX "/greet" location';
    }

    ## exact match
    location = /greet {
        return 200 'hello from NGINX "/greet" location';
    }

     ## regex match
    location ~ /greet[0-9] {
        return 200 'hello from NGINX "/greet" location';
    }

     ## regex match -case insensitive
    location ~* /greet[0-9] {
        return 200 'hello from NGINX "/greet" location';
    }
}
```

## variables

```
events {}

http {
    include mime.types;

    server {
        listen 80;
        server_name 52.66.247.22;

        root /data/www;

        set $weekend 'No';

        # check if weekend
        if ($date_local ~ 'Saturday|Sunday') {
            set $weekend 'Yes';
        }
    }

    location /inspect {
        return 200 $weekend;
    }
}
```

### rewrite and reload

```
events {}

http {
    include mime.types;

    server {
        listen 80;
        server_name 52.66.247.22;

        root /data/www;

        rewrite ^/user/(\w+) /greet/$1;
    location /greet {
        return 200 "Hello user";
        }
    }
}
```

### Master process and Worker process

* Master Process - Actual nginix serice or software instance.
* Worker process- Handle requests asynchronously.
```
worker_processes auto;
```

* This sets the number of connetions each worker process can accept.
* To check open file limit 'ulimit -n'
```
events {
    worker_connections 1024
}
```

### pid directive

```
eg: pid /var/run/new_nginx.pid;
```






