# install ftp

        - install
        sudo yum -y install vsftpd
        sudo service vsftpd start/stop/restart

        - check ftp config
        sudo vi /etc/vsftpd/vsftpd.conf
        sudo service vsftpd restart

        - add user
        sudo useradd -d /home/partner1 -s /sbin/nologin partner1  ->  can go to folder by sudo -su partner1
        sudo passwd partner1
            -> input welcome1 twice
        sudo vi /etc/vsftpd/user_list
        sudo service vsftpd restart

        - connect from local
        all this is ok to login from the server inside
        ftp localhost
        partner1
        welcome1

        enter 'passive' here to switch passive mode on/off
        - active mode is 'client: here is my number, call me please'
        - passive mode is 'client: may i have your number, let me call you'

        ls
        pwd
        cd /home
        ...

        - connect from outside
                - on o cloud, maybe need to add myrule to allow public internet access to default(iaas instance)
                - to be simple -> sudo service stop iptables
                - to be secured -> need to set iptable inside vm
                        iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
                        iptables -A INPUT -p tcp --dport 21 -j ACCEPT
                - use clear guest (or it cannot list folder)
                - test by ftp command from laptop, ftp ip...
                - test by ftp client, set folder to /home/partner1

        - limit user a specific foler
        - set sftp
        - troubleshoot
                - o cloud mft as ftp client -> iaas as ftp server

                - mft cloud
                do not close firewall because it needs port redirect
                change folder owner -> sudo chown o:o /mft -R

                - iaas
                it's ok to just stop firewall
                do not use /home/partner1 as source/target folder because some hidden files are there, can use /home/partner1/target

                - issue
                test ftp from mft cloud, as iaas is in inner network, it's sending back private ip to mft cloud to use.

                - fix in ftp server side:

                pasv_enable=YES
                port_enable=YES
                pasv_min_port=64000
                pasv_max_port=64100
                pasv_address=x.x.x.x
                pasv_addr_resolve=YES

                comment out listen_ipv6=YES
                change listen=NO -> listen=YES

                if you have firewall up, open port 20-21 for FTP, also enable passive ports to the range you specified above (pasv_min/max_port, eg: 64000-64100).
                Restart vsftpd.
