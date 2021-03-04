# check

- system

        cat /proc/version
        e.g.
        Linux version 3.10.0-957.21.3.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) ) #1 SMP Tue Jun 18 16:35:19 UTC 2019

        - redhat
        cat /etc/redhat-release

        - debian
        cat /etc/debian_version

- cores

        - centos
        grep -c ^processor /proc/cpuinfo

- memory

        free -h

- disk usage

        - df

            df -h

        - du 
            
            - current folder (s = summary, h = human read)
            du -sh

            - files in current folder
            du -sh *
            
            - show usage in tree, order desc
            du -h --max-depth=1 | sort -hr
            du -h --max-depth=2 | sort -hr

- network / port

        - check listening (port/process id/name)
        netstat -tulpn
        netstat -tulpn | grep LISTEN
        netstat -tulpn | grep :80

        e.g.
        netstat -tulpn | grep LISTEN
        // tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1095/sshd
        // tcp6       0      0 :::3306                 :::*                    LISTEN      14151/docker-proxy  
        // tcp        0      0 172.16.10.6:1521            0.0.0.0:*                   LISTEN      61926/tnslsnr

        - mac
        lsof -i -P -n | grep LISTEN
        // tnslsnr   61926   grid   15u  IPv4  755151      0t0  TCP 172.16.10.6:1521 (LISTEN)

        - telnet
        centos -> yum install telnet
        mac -> brew install telnet
        
        telnet localhost 8080
        
                1. listening
                trying ...
                connected

                2. not listening
                trying ...
                Connection refused

                3. firewall
                trying ...

- jvm

        - thread
        
                - high cpu pid
                top

                - high cpu thread pid
                top -Hp $PID

                - thread dump
                jstack $PID jstack.txt                

                - convert thread pid to 0x...
                e.g. 
                printf '%x\n' 133
                133 == 0x85

                - find thread stacktrace in jstack.txt
                e.g. 
                tid=0x0000085 ...
                at org.xxx.xxx

        - gc

                jstat -gcutil pidxxx 2000 10
                jmap -dump:format=b,file=./jmap.dump 13
                download
                open with Java VisualVM
                find large amout objects/class/leak suspects -> thread stacktrace

        - docker

                - hight cpu docker
                docker stats

                e.g.
                CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
                35b211b00041        admin               0.04%               835.4MiB / 7.375GiB   11.06%              655MB / 207MB       0B / 1.36MB         54

                - enter docker
                docker exec -it admin bash

                - copy from docker
                docker cp admin:/usr/local/tomcat/jstack.txt ./ 

        - core file
        
                - create
                kill -6 $PID

                - core file location
                cat /proc/sys/kernel/core_pattern

        - jcmd
        
                - check running jvm
                jcmd

                - help
                jcmd $PID help

                - check flags
                jcmd $PID VM.flags

                - 3 thread dumps
                jcmd $PID Thread.print > ~/thread01.txt
                jcmd $PID Thread.print > ~/thread02.txt
                jcmd $PID Thread.print > ~/thread03.txt

                - heap dump
                jcmd $PID GC.heap_dump ~/heap01.hprof

- find file

        - default path = current, detaul action = print
        find -name 1.json

        - path
        find /root -name 1.json

        - type
        find /root -type f -name 1.json
        find /root -type d -name myfolder

        - action, {} is the file found
        find /root -type f -name 1.json -exec echo "p=" {} \;

        


