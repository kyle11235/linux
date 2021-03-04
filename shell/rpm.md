# rpm

        - nameing
        e.g. pkgname-version.atchitecture.rpm

        - list all
        rpm -qa

        - find
        rpm -qa | grep -i packagename (-i ignore case)
        rpm -qa | tee /tmp/packagelist | grep packagename
        grep  packagename  /tmp/packagelist

        - check
        rpm -q packagename
        rpm -ql packagename (show included files)
        rpm -qi packagename (show desc)

        - install
        rpm -ivh packagename

        - delete
        rpm -e packagename
