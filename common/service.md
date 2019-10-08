# service

- place script

        e.g. cp logstash /etc/rc.d/init.d/

- create soft link (85 is priority)

        ln -s /etc/init.d/logstash /etc/rc.d/rc3.d/S85logstash
        ln -s /etc/init.d/logstash /etc/rc.d/rc4.d/S85logstash
        ln -s /etc/init.d/logstash /etc/rc.d/rc5.d/S85logstash

- or use chkconfig

        - auto enable 2,3,4,5
        chkconfig logstash on

        - close
        chkconfig logstash off

        - check status
        chkconfig --list logstash
