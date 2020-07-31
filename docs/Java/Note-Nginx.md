#### 前言
&emsp;&emsp;Nginx是一款由俄罗斯的程序设计师lgor Sysoev所开发高性能的Web和反向代理服务器，也是一个IMAP/POP3/SMTP代理服务器，在高并发的情况下，Nginx是Apache服务器不错的替代品。

#### 正文
- Nginx安装步骤（系统平台：CentOS release 7.0 64位）

```
1：将下载好的nginx-1.16.0.tar.gz压缩包上传到服务器
2：使用解压命令tar -xzvf nginx-1.16.0.tar.gz将压缩文件进行解压
3：安装gcc依赖，以用于压缩文件的编译使用
   yum install -y gcc-c++
   yum install -y pcre pcre-devel
   yum install -y zlib zlib-devel
   yum install -y openssl openssl-devel
4：编译nginx，先进入nginx解压后的目录，执行./configure命令为编译做好准备，执行完后目录下会生成一个Makefile文件
5：执行make PREFIX=/**命令进行编译，并指定安装后的目录，即可完成安装
```
- Nginx常用操作
```
1：先进入nginx安装目录下的sbin目录：cd /usr/local/nginx/sbin/
2：测试nginx配置文件是否配置正确：./nginx -t
3：启动nginx：./nginx
4：关闭nginx：./nginx -s stop (也可以采用直接查杀进程的方式)
5：退出nginx：./nginx -s quit  (等程序执行完毕后，建议使用此命令)
6：动态加载配置文件：./nginx -s reload (可以在不关闭nginx的情况下更新配置文件，使其生效)
7：虽然启动了nginx，但是默认除了linux系统自身的浏览器可以访问之外，其他的电脑还是访问不了，因为Centos的防火墙默认阻止22以外的所有端口，可以使用CentOs系统自带的firewall命令开启80端口，即可进行访问，访问成功页面如下。
````
- Nginx常用配置

```
#user nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    
    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        
        #中冶官网前端
        location / {
            root   C:/Users/YangKai/Desktop/dist-web;
            index  index.html index.htm;
        }
        
        #中冶官网后台
        location /admin {
            root   C:/Users/YangKai/Desktop;
            index  index.html index.htm;
        }
        
        location /api/ {    
                proxy_pass   http://127.0.0.1:8186/;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
        
        #上传
        location ^~ /UploadFiles/ {
           root   D:/static;
        }

        #上传
        location ^~ /image/ {
           root   D:/static;
        }

        #上传
        location ^~ /file/ {
           root   D:/static;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
    
    server {
        listen       10086;
        server_name  localhost2;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
                
        #中冶热工后台
        location / {
            root   C:/Users/YangKai/Desktop/dist;
            index  index.html index.htm;
        }
        
        #中冶热工前端
        location /app {
            root   C:/Users/YangKai/Desktop;
            index  index.html index.htm;
        }

        location /admin-api/ {
                proxy_pass   http://127.0.0.1:9010/;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
        
        location /wisave-api/ {
                proxy_pass   http://127.0.0.1:20110/;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
    #图片静态资源代理
    server {
       listen 10082;

       location / {
            root D:/static;
            autoindex on;
        }
    }

    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
    
    server {
        listen 8080;
        server_name localhost2;

    location / {
        root C:\Users\YangKai\Desktop\app123\app;
    }

    location /web/ {
        client_max_body_size 100m;
        proxy_pass http://10.0.0.166:9011/;
    }
    }
}
```