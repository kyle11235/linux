# setup ubuntu

- install

        - downlaod image
        - use balenaEtcher to flash image into 4GB USB
        - F12 when start system, choose to boot from USB

- wubi for 2 systems

        http://www.ubuntu.org.cn/download/ubuntu/windows-installer
        (This Windows installer (Wubi) will help you to run Ubuntu within your current system.)

        (http://mirrors.ustc.edu.cn/ubuntu-releases/12.10/)

        download wubi.exe
        uninstall by wubi.exe
- env
        
        files in /etc/profile.d are sourced by /etc/profile
        sudo vim /etc/profile.d/myenv.sh
        export JAVA_HOME=/u02/app/jdk1.8
        export PATH=$PATH:$JAVA_HOME/bin
        source it only effective for current shell, logout account for all

- git

        - install
        apt-get install git
        
        - git save password
        git config --global credential.helper store
        password is saved in ~/.git-credentials in plaintext
        
        - switch
        git config --global user.name "xxx"
        git config --global user.email "xxx@xxx.com"
        echo https://xxx:xxx@github.com >  ~/.git-credentials

- vim

        default vi in ubuntu is very strange
        apt-get install vim
        or you can change default vi to work like normal vi on other platform

- dash to bash

        sudo dpkg-reconfigure dash
        choose no (not as shell default tool)

- terminal copy paste

        - crtl + shift + c -> copy
        - crtl + shift + v -> paste to terminal
        - crtl + v -> paste to some editor

- ssh

        ssh kyle@x.x.x.x with the password for kyle user, do not ssh root user
        ssh_config is in /etc/ssh/ssh_config
 
- ngrok

        sudo -i
        npm install ngrok -g
        ngrok http 30002

- add package repository

        vi /etc/apt/sources.list
        e.g.
        deb http://ftp.de.debian.org/debian stretch main (for https://packages.debian.org/stretch/all/python3-usb/download)
        apt update

- install package manually (not recommanded, does not install dependency)

        e.g.
        wget http://ftp.us.debian.org/debian/pool/main/p/pyusb/python3-usb_1.0.0-1_all.deb
        dpkg -i python3-usb_1.0.0-1_all.deb
