# firewall

- firewalld VS iptables

        firewalld starts from centos7(RHEL7)
        firewalld uses iptables, it ues xml to manage rules(/usr/lib/firewalld and /etc/firewalld).
        while iptables uses file config (/etc/sysconfig/iptables)
        change of iptables re-read config file
        change of firewalld only changes different rule

- firewall-cmd VS firewalld

        firewall-cmd is the tool to manage firewalld

- change rule of firewalld

        sudo firewall-cmd --zone=public --permanent --add-port=9001/tcp
        sudo firewall-cmd --reload

- stop firewalld

        sudo systemctl stop firewalld
        sudo systemctl start firewalld
        sudo systemctl restart firewalld
        sudo systemctl enable firewalld (start as a system service)
