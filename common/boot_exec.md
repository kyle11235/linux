
- boot exec

        sudo vi /etc/rc.local
        e.g. sh /home/oracle/coredns/startdns.sh (rc.local will run as root, do not sudo in sh)
        
        sudo chmod u+x /etc/rc.d/rc.local
        sudo systemctl start rc-local.service
