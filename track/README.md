# track

        - download
        https://www.jetbrains.com/youtrack/download/get_youtrack.html

        - document
        https://www.jetbrains.com/help/youtrack/standalone/install-youtrack-jar.html


- install by jar

        use system jdk, faster than docker
        no luck in opc
        ok mac local, ali centos

        - prepare
        sudo -i
        systemctl stop firewalld (esc's stop by default)

        - download
        wget https://download.jetbrains.com/charisma/youtrack-2019.3.64616.jar
        install compatiable jdk

        - run
        ./run.sh
        tail out.log -f -n 100
        Wizard will be available on [http://hostname:8888?wizard_token=xxx] after start 

        - setup
        visit http://x.x.x.x:8888?wizard_token=xxx
        if host name in base url, change it to ip of host
        
        default location
        ~/teamsysdata
        ~/.youtrack/logs/
        ~/.youtrack/backups/

        - error (opc)
        hung at page - http://x.x.x.x:8888/projects/create
        [YouTrack Error] java.lang.IllegalStateException: s=COMPLETING i=false a=NOT_ASYNC

        - restore
        https://www.jetbrains.com/help/youtrack/standalone/Restore-JAR-Installation.html
        1. clear all in teamsysdata
        2. extract downloaded backup to teamsysdata
        3. run

        - stop / restart
        kill to stop first before using configure command to change anything
        to restart -> run wihtout params, will take previous params

        - uninstall
        rm -r ~/teamsysdata
        rm -r ~/.youtrack

- install by docker

        no luck in opc

        - guide
        https://hub.docker.com/r/jetbrains/youtrack

        - prepare
        sudo -i
        systemctl start firewalld (it will set rule)
        mkdir -p -m 750 /u02/app/youtrack/data /u02/app/youtrack/log /u02/app/youtrack/conf /u02/app/youtrack/backup 
        chown -R 13001:13001 /u02/app/youtrack/data /u02/app/youtrack/log /u02/app/youtrack/conf /u02/app/youtrack/backup (On macOS, do not perform chown)

        - run
        docker run -it --name youtrack  \
        -v /u02/app/youtrack/data:/opt/youtrack/data:Z \
        -v /u02/app/youtrack/conf:/opt/youtrack/conf:Z  \
        -v /u02/app/youtrack/log:/opt/youtrack/logs:Z  \
        -v /u02/app/youtrack/backup:/opt/youtrack/backups:Z  \
        -p 8888:8080 \
        jetbrains/youtrack:2019.3.64863

        Ctrl+PQ -> run in background
        docker logs youtrack -f

        - setup
        visit http://x.x.x.x:8888/?wizard_token=xxxx
        disable guest login, keep other params as is

        - stop
        docker exec youtrack stop
        
        - restore
        https://www.jetbrains.com/help/youtrack/standalone/restore-docker-image-installation.html

        1. stop and docker rm youtrack
        2. clear data and conf
        3. extract backup file into backup folder
        4. run and choose to upgrade from backup in setup page

        
- practice

        - team
        - as only 10 users, no need to manage users by group
        - create project -> team -> team roles -> change from default developer to reporter
        - project -> team -> add user -> change team member to assignee
        - user -> role -> grant user developer role if necessary
        
- reset root

        java -Djetbrains.charisma.restoreRootPassword=true -jar youtrack-2019.3.64616.jar 8888
        When YouTrack starts, the root user password and permissions are reset to their default values (root/root), login and set a new password for the account
        

