# iptables / port

- status/start/stop

        sudo service iptables start/stop
        sudo service iptables status

- check

        sudo iptables -t nat -L
        sudo iptables -S   ->  (check rule details)

- add/save/restart

        sudo iptables -I INPUT -p tcp --dport 8983 -j ACCEPT
        sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
        sudo iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 8443

        sudo service iptables save
        sudo service iptables restart

- check/delete

        1.delete by rule (rule 'INPUT -p tcp -m tcp --dport 21 -j ACCEPT', do not include -A used when you create the rule)
        sudo iptables -S
        sudo iptables -D INPUT -p tcp -m tcp --dport 21 -j ACCEPT

        2.delete by line number
        sudo iptables -t nat -L -n --line-numbers
        sudo iptables -t nat -D PREROUTING 1
        sudo iptables -t nat -D PREROUTING 1

- redirect port

        sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
        sudo iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 8443

- set accept host range

        sudo iptables -I INPUT -s 192.168.0.0/24 -p tcp --dport 1521 -j ACCEPT

