# package / compress

- gzip

        gzip file
        gunzip file.gz
        ...

- tarball

        - package whole dirname and compress
        tar czf myfile.tar.gz dirname

        - show content
        tar tzf myfile.tar.gz

        - uncompress
        tar xzf myfile.tar.gz

        - .tar.bz2, uncompress
        tar xjf myfile.tar.bz2
        
 - zip
 
        - zip only child files in my folder
        cd my
        zip -r my.zip *
        
        - zip my folder and child files
        zip -r my.zip my/
        
        
