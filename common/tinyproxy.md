
# tinyproxy / http proxy

- insntall

        sudo -i
        yum -y install tinyproxy

        cat /etc/tinyproxy/tinyproxy.conf > /home/opc/tinyproxy.conf
        chmod 777 /home/opc/tinyproxy.conf
        download

        comment out 'Allow 127.0.0.1' to allow any IP

        upload
        cat /home/opc/tinyproxy.conf > /etc/tinyproxy/tinyproxy.conf

        configure firewall to allow port 8888
        sudo firewall-cmd --zone=public --permanent --add-port=8888/tcp
        sudo firewall-cmd --reload

        systemctl start tinyproxy.service
        systemctl restart tinyproxy.service
        systemctl stop tinyproxy.service
        systemctl status tinyproxy.service   -> active (running)
        systemctl enable tinyproxy.service

- verify on the proxy server (failed)

        export http_proxy=
        export https_proxy=

        curl -x http://127.0.0.1:8888 https://google.com
        curl -x https://x.x.x.x:8888 https://google.com

- set proxy on client PC (failed)

        export http_proxy=
        export https_proxy=
        export http_proxy=x.x.x.x:8888
        export https_proxy=x.x.x.x:8888
        curl https://google.com
