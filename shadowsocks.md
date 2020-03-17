
# shadowsocks

        socks5 proxy
        https://shadowsocks.org (download/config)
        https://github.com/shadowsocks

- client

        https://github.com/shadowsocks/shadowsocks-android/releases/download/v5.0.5/shadowsocks--universal-5.0.5.apk

- server

        - install
        sudo -i
        wget –no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-go.sh
        chmod +x shadowsocks-go.sh
        ./shadowsocks-go.sh 2>&1 | tee shadowsocks-go.log

        default port=9558
        password=xxx
        default cipher=aes-256-cfb

        - config
        vi /etc/shadowsocks/config.json

        - uninstall
        sudo -i
        ./shadowsocks-go.sh uninstall

        - usage
        /etc/init.d/shadowsocks start
        /etc/init.d/shadowsocks stop
        /etc/init.d/shadowsocks restart
        /etc/init.d/shadowsocks status

        - firewall
        yum install firewalld
        systemctl start firewalld
        systemctl stop firewalld
        systemctl disable firewalld // disable auto start

        - port
        firewall-cmd --list-ports
        firewall-cmd --zone=public --add-port=9558/tcp --permanent
        firewall-cmd --zone=public --add-port=9558/udp --permanent
        firewall-cmd --reload

-dns

        try use 8.8.8.8 instead of dns.google
        
- ssh
        
        mobile/pc on same wifi
        
        - pc
        port from=9558
        host to=127.0.0.1
        port to=9558
        bind address=0.0.0.0 (not 127.0.0.1)
        
        - mobile
        pc ip:9558
        
        
