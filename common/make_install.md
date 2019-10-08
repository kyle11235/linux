# make install

        - download unpackage
        mkdir pkgdir
        cd pkdir
        tar xvzf package.tar.gz (for gzip file)
        tar xvjf package.tar.gz (for bzip2 file)

        - check insntall or readme
        less INSTALL

        - check and backup config
        ./configure -help | tee /tmp/cfgopt  

        - configure
        ./configure options

        - compile
        make

        - install
        make install
