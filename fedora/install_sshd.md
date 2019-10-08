# fedora15 sshd

      su -
      yum install openssh-server

      1> check status
      /sbin/service sshd status

      2> start ssh server
      /sbin/service sshd start

      service sshd start

      /etc/init.d/sshd stop
      /etc/init.d/sshd start
      /etc/init.d/sshd restart

      3> configure ssh
      vi /etc/ssh/ssh_config, uncomment below
      Port 22
      Protocol 2,1
      service sshd restart

      4> enable auto start
      vi /etc/rc.local
      /etc/init.d/sshd start

      5> configure firewall
      by UI or /usr/bin/system-config-firewall

      /etc/init.d/iptables stop
      /etc/init.d/iptables start
