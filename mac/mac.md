# mac

- setup

        - finder
        change finder defualt open location
        finder -> advanced -> show file extensions
        
        expand save dialog default
        defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true
        defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true
        
        - new file
        automator -> quick action/service -> utils -> run applescript -> no input, Finder -> save as New README.md
        if delete workflow, it's in ~/Library/Services
        
        tell application "Finder"
                set txt to make new file at (the target of the front window) as alias with properties {name:"README.md"}
                select txt
        end tell
        
        keyboard -> shortcut -> service -> command + option + N (no conflict)
        enable by a run, Finder -> services -> New README

        - new terminal at folder
        keyboard -> shortcut -> service -> new terminal at folder -> command + option + J (no conflict, consistent with vscode)
        
        - wifi
        chrome -> https://vsupport.xxx.com/wifi
        enalbe auto proxy discovery for corporate network
        
        - printer
        https://printers.xxx.com -> printer -> linux tab -> hostname e.g. xxx16b.cn.zzz.com
        printers & scanners -> + -> IP
        fill in hostname and choose 'use generic PCL printer'
        
        - outlook
        https://stbeehive.xxx.com/zimbra/
        stbeehive.xxx.com/smtp ssl / 465, 993 / normal password
        
        - common
        for system integrity protect, unable to create /u02 anymore in bit sur
        chmod 755 /etc/profile (or cannot edit it even root)
        editor = visual code
        screenshot = lightshot
        installer = home brew
        ssh = termius
        ftp = filezilla
        unpackage = Dr. unarchivier
        backup = freeFileSync
        compare files = diffmerge
        svn client = snailSVNlite
        vpn
        git is included in xcode tools
        nodejs by mac installer
        jdk by mac installer (export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_281.jdk/Contents/Home)
        maven by zip file
        gradle by sdkman
        
        - disable dock bouncing
        defaults write com.apple.dock no-bouncing -bool TRUE
        killall Dock (relaunch dock)
        
        
- key

        Hide window= command + h (do not use command + m)
        show window = command + tab

        sleep = control + shift + power (old)
        sleep = control + command + q (new)

        show Icon = command + 1
        show List = command + 2
        show Tree = command + 3

        Go parent = command + up
        Go child = command + down
        Go previous = command + [

        show desktop = command + F3
        show/hide hidden files = command + shift + .

- vi

        go to end of file -> ESC mode -> G

- chrome

        New chrome tab = command + t
        Switch tab = ctrl + tab
        Close window = command + w
        refresh = command + r
        copy url = command + L
        open inspector = command + alt + j

- eclipse

        go back/forward position = alt + command + left/right
        format width = preference -> java -> code format -> search width
        
- imovie

        - video
        trim video = window -> show clip trimmer -> drag

        - title
        add title = Titles -> click where to add -> double click a title
        adjust title duration = click info icon (!) / drag
        edit text = double click title, change font / size / color -> click icon V to apply
        move title lower using = new line / option + enter
        
        - internal audio record
        download Soundflower from https://github.com/mattingalls/Soundflower/releases
        audio MIDI setup -> create Multi-output Device -> select builtin + soundflow(2ch) -> 
        system preference -> sound -> output select multi-output device
        quicktime -> file -> audio record -> select soundflow as input

- homebrew

        vi /etc/hosts to allow access to github content site
        e.g.
        192.30.253.112    Build software better, together 
        192.30.253.119    gist.github.com
        151.101.184.133    assets-cdn.github.com
        151.101.184.133    raw.githubusercontent.com
        151.101.184.133    gist.githubusercontent.com
        151.101.184.133    cloud.githubusercontent.com
        151.101.184.133    camo.githubusercontent.com
        151.101.184.133    avatars0.githubusercontent.com
        151.101.184.133    avatars1.githubusercontent.com
        151.101.184.133    avatars2.githubusercontent.com
        151.101.184.133    avatars3.githubusercontent.com
        151.101.184.133    avatars4.githubusercontent.com
        151.101.184.133    avatars5.githubusercontent.com
        151.101.184.133    avatars6.githubusercontent.com
        151.101.184.133    avatars7.githubusercontent.com
        151.101.184.133    avatars8.githubusercontent.com

        install
        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

