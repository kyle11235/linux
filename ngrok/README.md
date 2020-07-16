
- run

        vpn
        ngrok http 8080

- ubuntu

        sudo -i
        npm install ngrok -g
        ngrok http 30002
        
- linux

        wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
        ./ngrok authtoken xxx (if not sign in and get this token, it will expires 1 day)
        nohup ./ngrok http 8000 > /dev/null &
        curl http://127.0.0.1:4040/api/tunnels
        
