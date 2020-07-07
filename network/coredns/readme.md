

- coredns

        sudo vim /etc/sysconfig/selinux
        SELINUX=xxx -> SELINUX=disabled

        - vm-0

                - dns resolver
                sudo vi /etc/resolv.conf (lost after reboot)
                nameserver 10.0.2.15

                sudo vi /etc/docker/daemon.json
                "dns":["10.0.2.15", "8.8.8.8"]
                
                - hostname
                sudo hostnamectl set-hostname vm-0.example.com
                hostname -> vm-0.example.com

                sudo vi /etc/hosts
                10.0.2.15 vm-0.example.com

        - vm-1
        
                - hostname
                sudo hostnamectl set-hostname vm-1.example.com
                hostname -> vm-1.example.com

                sudo vi /etc/hosts
                10.0.2.4 vm-1.example.com

        - start
        
                cd coredns
                vi Corefile

                chmod +x coredns
                chmod +x startdns.sh
                sudo ./startdns.sh

        - boot start
        
                sudo vi /etc/rc.local
                sh /home/oracle/coredns/startdns.sh (not work)

