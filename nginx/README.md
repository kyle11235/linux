# nginx

- oracle iaas linux 7.6, yum

        sudo -i
        firewall-cmd --zone=public --permanent --add-port=80/tcp
        firewall-cmd --zone=public --permanent --add-port=443/tcp
        firewall-cmd --reload
        yum install -y nginx (/sbin/nginx, /etc/nginx/nginx.conf, /usr/share/nginx/html)
        nginx (start nginx)
        
        if change html folder to /home/opc/app
        change 'user nginx' to 'user root' of /etc/nginx/nginx.conf

- ali ec2 centos, yum

        yum install -y nginx (/sbin/nginx, /etc/nginx/nginx.conf, /usr/share/nginx/html)
        nginx (start nginx)

- oracle iaas, source file

        tar -zxvf nginx-1.8.1.tar.gz
        cd nginx-1.8.1
        ./configure

        C compiler cc is not found:
        sudo yum install gcc gcc-c++ ncurses-devel perl


        sudo yum install pcre-devel
        ./configure --without-http_gzip_module --prefix=/u02/app/nginx

        or

        ./configure --without-http_rewrite_module --without-http_gzip_module --prefix=/u02/app/nginx

        make
        sudo make install
        sudo chown opc:opc /u02/app/nginx -R
        vi /u02/app/nginx/conf/nginx.conf

        access_log off;

        location ^~ /hcm {
            proxy_pass   http://127.0.0.1:8080;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }

        sudo /u02/app/nginx/sbin/nginx

- ubuntu

        http://wiki.ubuntu.org.cn/Nginx
        sudo apt-get install nginx

        /usr/sbin/nginx
        /etc/init.d/nginx
        sudo /etc/init.d/nginx start

        /etc/nginx/nginx.conf
        /var/www/nginx-default or /var/www
        /var/log/nginx

- mac

        brew install nginx 
        brew services start nginx
        http://localhost:8080
        /usr/local/Cellar/nginx/x.x.x/html
        brew services restart nginx









