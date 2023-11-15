# Technical Articles
<p align="center">
  <a href="https://github.com/madxradicle/madxframework2.0">
    <img src="https://github.madxradicle.com/MR_logo.png" alt="Logo" width="200px" height="100px">
  </a>
  <h3 align="center">Technical Articles</h3>
  <p align="center">
   These articles are initially written in chinese and they're moved from google documents.
    <br />
    <a href="https://github.com/madxradicle/articles"><strong>Explore the docs »</strong></a>
    <br />
    <a href="https://github.com/madxradicle/articles/issues">Report Bug</a>
    ·
    <a href="https://github.com/madxradicle/articles/issues">Request Feature</a>
  </p>
</p>

# The cloudflare A name and cpanel setup
113.52.132.214 CDN SERVER IP

161.202.26.249 CPANEL SERVER IP

# server nginx setting
1. Create a origin domain for reverse proxy, I parked 3 more domains in cPanel, and point them Cloudflare. Do not enable the Cloudflare proxy
	origin-member.freechats.net 161.202.26.249
	origin-admin.freechats.net 161.202.26.249
	origin-public.freechats.net 161.202.26.249
 
2. Nginx config under upstream block connect to origin domain
```
upstream origin-server.madxpanel.com.pool
    {
        server origin-member.freechats.net:80 weight=10 max_fails=3;
        server origin-admin.freechats.net:80 weight=10 max_fails=3;
        server origin-public.freechats.net:80 weight=10 max_fails=3;
    }
```
# Cloudflare setting
3. CDN domain point to CDN server in Cloudflare. Do not enable the Cloudflare proxy
```
	public-fc.freechats.net 113.52.132.214
	admin-fc.freechats.net 113.52.132.214
	member-fc.freechats.net 113.52.132.214
```
4. Real domain CNAME to CDN domain in Cloudflare. Do not enable the Cloudflare proxy
```
content >public-fc.freechats.net >CNAME >public
Content >member-fc.freechats.net >CNAME >member 
content > admin-fc.freechats.net >CNAME >admin
```

# Prepare CDN Server: buy VPS server get id and password for Server

# Use Putty access server CND

at root use login interface

Below just enter the command

# CHeck the ip infomation

curl ipinfo.io


# Change the server name CDN-server

hostnamectl set-hostname CDN-server


# Change time and date to Kuala lumpur

timedatectl set-timezone "Asia/Kuala_Lumpur"


# stop firewall service and disable on boot

systemctl stop firewalld && systemctl disable firewalld

setenforce 0

sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux

getenforce


# update Centos package and install nginx

yum install epel-release -y

yum groupinstall "development tools" -y

yum install vim wget lrzsz unzip yum-utils iptables-services net-tools lsof nano -y

yum install nginx -y


# enable iptables firewall rules and put iptables as firewall in root folder

cd ~

mkdir /root/bin/

touch /root/bin/iptables.sh && chmod 744 /root/bin/iptables.sh



# put iptables everyrules on it

nano /root/bin/iptables.sh

# copy below and paste inside

请copy以下写法：
```sh
#!/bin/sh
echo "1" > /proc/sys/net/ipv4/ip_forward
SshPort=22
/sbin/iptables -F
/sbin/iptables -t nat -F

#allow local
/sbin/iptables -A INPUT -i lo -j ACCEPT
/sbin/iptables -A INPUT -s 127.0.0.1 -j ACCEPT

#softlayer subnet range
/sbin/iptables -A INPUT -s 10.93.100.128/26 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 10.117.3.192/26 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 10.193.72.64/26 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 10.67.125.64/26 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 119.81.54.0/28 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 119.81.205.128/26 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 161.202.25.40/29 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 161.202.26.240/28 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 161.202.201.0/27 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 165.192.88.32/28 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 169.60.39.208/28 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 119.81.59.32/29 -j ACCEPT #IBM_RANGE
/sbin/iptables -A INPUT -s 121.122.73.0/16 -j ACCEPT #MY HOME RANGE
/sbin/iptables -A INPUT -s 113.52.128.0/20 -j ACCEPT #Freechat net

#allow port
/sbin/iptables -A INPUT -p tcp -m tcp --dport  $SshPort -j ACCEPT #ssh
/sbin/iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT #http
/sbin/iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT #https

/sbin/iptables -A INPUT -p icmp -m limit --limit 1/s --limit-burst 10 -j ACCEPT
/sbin/iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
/sbin/iptables -A INPUT -m state --state INVALID,NEW -j DROP

/sbin/iptables-save

```


# Install our iptables script to run when server start
# And make sure you at root/bin/ folder if not sure you can type pwd check location

pwd

# run one time iptables

./iptables.sh


# now put the script run on crontab

crontab -e


# add below

@reboot /root/bin/iptables.sh


# turn on service in boot and start it

systemctl status iptables

systemctl start iptables

systemctl enable iptables

systemctl status iptables


#2. Step to install nginx to reverse proxy

systemctl start nginx


# check on your browser and type the http://CDN_IP  see the website got http running there will say Welcome to CentOS, so it was normal on nginx

#next GO to nginx folder

cd /etc/nginx/


# list it see got nginx.conf or not, if yes backup default nginx.conf

ls

cp nginx.conf nginx.conf_bak


# doble check nginx.conf_bak if got  then only edit nginx.conf

ls


# use nano easy to edit nginx.conf, make sure delete everything in nginx.conf

nano nginx.conf

# put below this on nginx.conf
**Note**

**Copy this below to nginx.conf：**
```sh

# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;
    server_tokens off;
    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
#    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/conf.d/chan_cdn.conf;
#    include /etc/nginx/conf.d/cdn/cannon_cache.conf;
}
```

# Next go to conf.d folder, make sure you at /etc/nginx folder can use pwd
pwd

# copy the ssl to folder, and make sure in /etc/nginx
mkdir -p /etc/nginx/ssl

# use filezilla upload all ssl file to this folder, something like this
STAR_freechats_net (1)        STAR_freechats_net.crt  STAR_freechats_net.key
STAR_freechats_net.ca-bundle  STAR_freechats_net.csr  STAR_freechats_net.zip  

# Next go back to nginx folder, make sure you at /etc/nginx folder can use pwd#
cd /etc/nginx
pwd

# now GO to conf.d folder
cd conf.d

# so at here type  nano chan_cdn.conf , to copy paste this file
nano chan_cdn.conf

```sh
#---upstream settings
upstream origin-server.freechats.net.pool
    {
        server origin-member.freechats.net:80 weight=10 max_fails=3;
        server origin-admin.freechats.net:80 weight=10 max_fails=3;
        server origin-public.freechats.net:80 weight=10 max_fails=3;
}



#---cdn settings[https]
proxy_temp_path /opt/nginx_cache/proxy_temp_dir;
proxy_cache_path /opt/nginx_cache/proxy_cache_dir levels=1:2 keys_zone=cdn_madxpanel:50m inactive=1d max_size=1g;


server
    {
        listen 80;
        server_name public-fc.freechats.net admin-fc.freechats.net member-fc.freechats.net;
        access_log /var/log/nginx/cannon_cdn.access.log;
        error_log /var/log/nginx/cannon_cdn.error.log;

        return 301 https://$host$request_uri;
}

server
    {
        listen 443 ssl;
        server_name public-fc.freechats.net admin-fc.freechats.net member-fc.freechats.net;

        ssl_certificate /etc/nginx/ssl/STAR_freechats_net.crt;
        ssl_certificate_key /etc/nginx/ssl/STAR_freechats_net.key;
        access_log /var/log/nginx/ssl_cannon_cdn.access.log;
        error_log /var/log/nginx/ssl_cannon_cdn.error.log;


location ~ .*\.(gif|jpg|png|html|htm|css|js|ico|swf|pdf)$
    {
        include conf.d/cache_conf/static_cache.conf;
  }


location /
    {
        include conf.d/cache_conf/other_cache.conf;
  }

if ($http_user_agent ~* (curl|wget|WordPress))
    {
        return 403;
  }

if ($request_method !~ ^(GET|HEAD|POST)$ )
    {
        return 405;
  }

}
```

# after edit go make new folder call cache_conf
mkdir cache_conf
# go to folder inside and make 2 file
cd cache_conf/

nano other_cache.conf

```sh
        proxy_redirect off;
        proxy_next_upstream http_502 http_504 http_404 error timeout invalid_header;
        proxy_set_header Host $host;
        proxy_set_header X-real-ip $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://origin-server.freechats.net.pool;
        client_max_body_size 40m;
        client_body_buffer_size 128k;
        proxy_connect_timeout 60;
        proxy_send_timeout 60;
        proxy_read_timeout 60;
        proxy_buffer_size 64k;
        proxy_buffers 4 32k;
        proxy_busy_buffers_size 64k;

```

# save and exit, then nano static_cache.conf
nano static_cache.conf

```sh
           #Proxy
        proxy_redirect off;
        proxy_next_upstream http_502 http_504 http_404 error timeout invalid_header;
        proxy_set_header Host $host;
        proxy_set_header X-real-ip $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://origin-server.freechats.net.pool;

        #Use Proxy Cache
        proxy_cache_revalidate on;
        proxy_cache cdn_madxpanel;
        proxy_cache_key "$host$request_uri";
        add_header Cache "$upstream_cache_status";
        proxy_cache_valid  200 304 301 302 8h;
        proxy_cache_valid 404 1m;
        proxy_cache_valid  any 2d;
        proxy_buffers 256 16k;
        proxy_buffer_size 32k;
        add_header MADX-CDN-Cache "$upstream_cache_status";
        expires 5m;
        proxy_cache_background_update on;

```

# save and exit, verify nginx -t should get any error
nginx -t

# there are missing some file folder, so go create now
mkdir -p /opt/nginx_cache/proxy_temp_dir
mkdir -p /opt/nginx_cache/proxy_cache_dir

# then double check nginx, now should be ask you to restart nginx service
nginx -t
# restart nginx and now should test your cdn was proxy it
systemctl restart nginx

# Can use your windows machine cmd
 ping -c 5 admin.freechats.net

# you also can check the error here
tail -f 20 /var/log/nginx/ssl_cannon_cdn.error.log*

# make sure to turn on boot nginx
systemctl enable nginx
