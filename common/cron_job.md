
# cron job

- list jobs in /etc/crontab

        [opc@my ~]$ sudo -i
        [root@my ~]# ls /etc/crontab
        /etc/crontab
        [root@my ~]# cat /etc/crontab
        SHELL=/bin/bash
        PATH=/sbin:/bin:/usr/sbin:/usr/bin
        MAILTO=root

        # For details see man 4 crontabs

        # Example of job definition:
        # .---------------- minute (0 - 59)
        # |  .------------- hour (0 - 23)
        # |  |  .---------- day of month (1 - 31)
        # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
        # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
        # |  |  |  |  |
        # *  *  *  *  * user-name  command to be executed

        0 0,12 * * * root python -c 'import random; import time; time.sleep(random.random() * 3600)' && /usr/local/bin/certbot-auto renew
        [root@my ~]#

- create a job

        - call python
        echo "0 0,12 * * * root python -c 'import random; import time; time.sleep(random.random() * 3600)' && /usr/local/bin/certbot-auto renew" | tee -a /etc/crontab > /dev/null

        - call shell
        echo "0 * * * * root bash -c 'echo hello > /u02/app/hello'" | tee -a /etc/crontab > /dev/null

- remove

- other

        sleep
        watch
        at
        crontab
