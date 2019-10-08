
# export

- show env

        printenv   or env

- desc

        export makes a variable something that will be included in child process environments.
        It does not affect other already existing environments.
        In general there isn't a way to set a variable in one terminal
        and have it automatically appear in another terminal, the environment
        is established for each process on its own.

        Adding it to your .profile makes it so that your environment will be setup to include that new variable each time you log in though. So it's not being exported from one shell to another, but instead is instructing a new shell to include it when it sets up the initial environment.

        MYVAR=1001
        export MYVAR

- export

        - temp var for 1 command
        MYVAR=1001 echo $MYVAR

        - user shell
        /etc/bashrc

        - user login
        ~/.bash_profile
        source ~/.bash_profile

        - user logout
        ~/.bash_logout

        - system startup
        /etc/profile
