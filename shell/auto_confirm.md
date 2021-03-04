# auto confirm

- confirm

        echo "Y Y N N Y N Y Y N" | ./your_script

        cat "input.txt" | ./your_script

        yes Y | ./your_script

        yes N | ./yout_script

- root password (not work!)

        cat /etc/sudoers
        visudo -f sudoers
        kyle ALL=(ALL) NOPASSWD: /usr/local/bin/vpn or %admin ALL=(ALL) NOPASSWD: /usr/local/bin/vpn
