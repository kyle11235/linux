
# Reverse Proxy

        - guide
        https://www.jetbrains.com/help/youtrack/standalone/Reverse-Proxy-Configuration.html

        1. kill

        2. change base-url
        different from the official guide, i'm using /pm to diff from other projects
        
        java -jar youtrack-2019.3.64616.jar configure --listen-port 8888 --base-url https://www.example.com/pm

        3. update nginx.conf
                
        worker_rlimit_nofile 65535
        events {
            worker_connections 2048;
        }

        ...

        # for youtrack
        location /pm {
            proxy_pass http://localhost:8888; # without tail /, keep pm in path
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;

            proxy_set_header X-Forwarded-Host $http_host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            
            # proxy_buffer_size 64k;
            client_max_body_size 10m;

            proxy_http_version 1.1;
        }

        location /pm/api/eventSourceBus {
            proxy_pass http://localhost.com:8888;
            proxy_cache off;
            proxy_buffering off;
            proxy_read_timeout 86400s;
            proxy_send_timeout 86400s;
            proxy_set_header Connection '';
            chunked_transfer_encoding off;

            proxy_set_header X-Forwarded-Host $http_host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;

            proxy_http_version 1.1;
        }

        4. start without params
        java -jar youtrack-2019.3.64616.jar > out.log 2>&1 &

        tail -f out.log -n 100
        will be available on [https://www.example.com/pm/bundle/starting] after start 
