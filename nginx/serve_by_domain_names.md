# by domain name

        0.install nginx with http_rewrite_module


        1.add this part before location / {...}

        server_name ~^(?<subdomain>\w*?)?\.?(?<domain>\w+\.\w+)$;

        location / {
            root "/u02/app/nginx/html/$domain/web";
            index index.html;
        }

        2.alternatively, you can use www or dynamic sub domains

        server_name ~^(?<subdomain>\w*?)?\.?(?<domain>\w+\.\w+)$;

        if ($subdomain = "") {
            set $subdomain "www";
        }

        if (!-d "/u02/app/nginx/html/$domain/$subdomain") {
            set $subdomain "www";
        }

        location / {
            root "/u02/app/nginx/html/$domain/$subdomain";
            index index.html;
        }


        3.delete location / {...}


        4.prepare html
        /u02/app/nginx/html/jinshou.com/web

        5.test
        sudo vi /etc/hosts
        127.0.0.1  jinshou.com www.jinshou.com

        curl jinshou.com
        curl www.jinshou.com
