# install mysql - 20131204

    download mysql-5.5.10-linux2.6-i686.tar.gz
    or download zip and unzip it

- unpackage

    sudo -i
    cd /usr/local
    tar zxvf path/mysql-5.5.10-linux2.6-i686.tar.gz
    ln -s mysql-5.5.10-linux2.6-i686 mysql

- group

    groupadd mysql
    useradd -r -g mysql mysql
    chown -R mysql .
    chgrp -R mysql .

- install

    scripts/mysql_install_db --user=mysql --basedir=/usr/local/mysql

    if - error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
    apt-get install libaio-dev

    chown -R root .
    chown -R mysql data
    cp support-files/my-medium.cnf /etc/my.cnf

- start

    cp support-files/mysql.server  /etc/init.d/mysql
    /etc/init.d/mysql restart | start

- login

    bin/mysql -uroot (no password)
    bin/mysql -uroot mysql
    update user set password=password('xxx') where user='xxx';
