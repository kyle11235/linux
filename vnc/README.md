# vnc

- install on debian 8

        - install
        apt-get update
        apt-get -y upgrade
        apt-get install xfce4 xfce4-goodies gnome-icon-theme tightvncserver
        apt-get install iceweasel (optional install browser)

        - add user
        adduser vnc
        passwd vnc

        - grant sudo
        apt-get install sudo
        gpasswd -a vnc sudo

        - start vnc server
        su - vnc
        vncserver (set password)
        e.g. New 'X' desktop is vnc:1

        - check port
        cd /home/vnc/.vnc
        cat debian\:2.pid
        e.g. 5624, by default first is 5901

        - connect
        vnc viewer -> ip:pid_number
        e.g. ip:2

        - kill server
        vncserver -kill:1

- auto start service

        - create service script
        nano /usr/local/bin/myvncserver

        #!/bin/bash
        PATH="$PATH:/usr/bin/"
        DISPLAY="1"
        DEPTH="16"
        GEOMETRY="1024x768"
        OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"

        case "$1" in
        start)
        /usr/bin/vncserver ${OPTIONS}
        ;;

        stop)
        /usr/bin/vncserver -kill :${DISPLAY}
        ;;

        restart)
        $0 stop
        $0 start
        ;;
        esac
        exit 0

        chmod +x /usr/local/bin/myvncserver

        /usr/local/bin/myvncserver start
        /usr/local/bin/myvncserver stop
        /usr/local/bin/myvncserver restart

        - create unit file
        nano /lib/systemd/system/myvncserver.service
        [Unit]
        Description=Manage VNC Server on this droplet

        [Service]
        Type=forking
        ExecStart=/usr/local/bin/myvncserver start
        ExecStop=/usr/local/bin/myvncserver stop
        ExecReload=/usr/local/bin/myvncserver restart
        User=vnc

        [Install]
        WantedBy=multi-user.target

        - enable service
        systemctl daemon-reload
        systemctl enable myvncserver.service

        - usage
        systemctl start myvncserver.service
        systemctl stop myvncserver.service
        systemctl restart myvncserver.service

- secure with ssh tunnel

        systemctl stop myvncserver.service
        nano /usr/local/bin/myvncserver (change to localhost)
        OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY} -localhost"
        systemctl start myvncserver.service
