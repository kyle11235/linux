
# enable sshd

1./etc/init.d/sshd start

2.iptables -I INPUT -p tcp --dport 22 -j ACCEPT

3.passwd root new password

        useradd xxx
        passwd xxx -> xxx

        vi /etc/ssh/sshd_config
        uncomment -> PasswordAuthentication yes
        commnent out ->PasswordAuthentication no

        restart sshd:
        service sshd restart (this will call below command)
        or systemctl restart sshd.service

        then you can login with xxx/xxx

3.windows friewall
