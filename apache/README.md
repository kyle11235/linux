- ubuntu

        apt-get apache2
        service apache2 status
        service apache2 start = /etc/init.d/apache2 start

        - config
        /etc/apache2/apache2.conf

- mac

        pre-installed
        apachectl -v
        php -v
        sudo apachectl start/stop/restart

        sudo cp /etc/apache2/httpd.conf /etc/apache2/httpd.conf.origin
        sudo vi /etc/apache2/httpd.conf
        DocumentRoot "/Library/WebServer/Documents"
        DirectoryIndex index.html index.php
        ...

        sudo apachectl restart
        http://localhost