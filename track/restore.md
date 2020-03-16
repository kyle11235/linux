
- restore backup from https://www.example.com/pm

        1. try with non-root user
        clear all in ~/teamsysdata
        extract backup to ~/teamsysdata
        java -jar youtrack-2019.3.64616.jar --no-browser 8888/pm -> Failed to create logs directory: /root/.youtrack/logs
        cause backup is from root user installation

        2. try with root
        sudo -i
        java -jar youtrack-2019.3.64616.jar --no-browser 8888/pm -> JetBrains YouTrack 2019.3 Configuration Wizard will be available on [http://xxx.local:8888/pm?wizard_token=xxx] after start
        now, it starts as root user, but extracted backup is not under root user, so open wizard to restore

        open with localhost, http://localhost:8888/pm?wizard_token=xxx
        click upgrade (the other one is setup)

                - Upgrade
                Before you continue, read the upgrade instructions.
                The instructions contain important guidelines that you need to follow to ensure that your YouTrack installation is upgraded successfully.
                To upgrade from a backup, select the location of a compressed backup file or the directory of an unzipped backup.
                To upgrade from an existing YouTrack installation, select the location of the installation directory.

                - Restore
                To restore your YouTrack installation from a backup, select the location where the ZIP file or unzipped backup is stored.

        select where extracted backup is
        e.g. /Users/kyle/teamsysdata

        change base url from https://www.example.com/pm to http://localhost:8888/pm

        restore successfully!
        253 issues backup = 16.6M

        login with existing user/password

- restore backup from https://www.example.com/pm or http://x.x.x.x:8888/pm

        sudo -i
        java -jar youtrack-2019.3.64616.jar --no-browser 8888/pm
        http://localhost:8888/pm?wizard_token=MZNyTWq6tX2IzYrk9AYO
        click upgrade
        select /Users/kyle/Downloads/tsky_backup
        change base url from https://www.example.com/pm to http://localhost:8888/pm
        restore successfully!
        login with existing user/password
