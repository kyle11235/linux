# network

- HUB vs Switch vs Router

        - HUB is stupid copy to all
        - Switch is smart, direct data to single port based on mac address
        - Router
        HUB/Switch are only for Local Area Network/LAN
        Router can read IP, so it can be used for Wide Area Network/WAN, when external network is involed, it’s called Gateway!
        192.168.10.10 <-> (192.168.10.1,172.16.10.1) <-> 172.16.10.20

- OCI Cloud Networking

        - VCN
        VCN created by admin copied to all compartments
                
                - Subnet
                subnet is real worker of VCN
                subnet best to be across 3 AD, simple and reasonalble
                CIDR define IP segment

                        - Security List
                        - DHCP Options
                        - Route Table (only required for non CIDR range IP request)
                                
                                - route rule
                                specify destination CIDR block and the target (next hoop)
                                allowed target type including
                                
                                        - various gateways
                                        - private IP
        
                - Internet Gateway
                - NAT Gateway
                - Service Gateway
                - Dynamic Routing Gateway / DRG
                - Local Peer Gateway / LPG

        - Customer-Premise Equipment
        - IPSec Connection
        - FastConnect
        - Public IPs
        - LB

- DHCP

        client-server model, DHCP client request, and DHCP server manage IP pool and assign IP for clients

- NAT

        Network Address Translation
        private <-> NAT <-> public
    
        https://www.virtualbox.org/manual/ch06.html#network_nat_service

        - NAT between host and guest VM
        NAT(not NAT network)

        1. from guest to visit host

            check ip from host
            1.try to use the local connection IPV4
            2.try default mask

        2. from host to guest

            1.port forwarding(not working for my own test vm, but works for mft+osb vm)
            2.ip + host setting?

        3. from guest to visit external network

            1.in office, use wireless account
            2.at home, ok directly

- file sharing between PC

        disable ipv6 on windows
        enable service SMP1.0 on windows
        smb://10.7.23.81
        ... not finished

- connect 2 tp
        
        
        首先A路由器不管,就按原来设置上网什么的就行了,不要开启WDS,记下A路由器得到的DNS服务器地址下文有用 (注意是dns 有两个 切记)
        进入A路由器的DHCP服务器设置,把结束地址池的地址改为:192.168.1.150[防止待会儿B路由器的地址冲突]),同时A路由设置一个固定的信道,看你自己喜欢了

        进入B路由(设置前最好恢复一次出厂设置)[为了防止路由器地址冲突,最好把B路由的IP地址改为192.168.1.2或其他],工作模式随便了,个人喜欢动态IP
        在无线设置里面开启WDS,扫描路由A的SSID并填写好相关的信道,加密方式,和密钥.
        完成后保存
        
        在进入B路由的DHCP服务器设置,(这里可是很多同学不能上网的原因所在),
        B路由器的DHCP服务器一定要开启,否则就别上网了
        起始地址池填192.168.1.151
        结束地址池填192.168.1.199
        网关填路由器A的IP地址:192.168.1.1
        缺省域名:不填
        主DNS服务器:a的（刚刚提到的那个DNS第一个）
        备用DNS服务器:a的（刚刚提到的那个DNS第二个）
        保存并重启
        注:很多童学在开WDS的时候因为关闭了B路由DHCP服务器,导致不能获取到IP地址而上不了网

- network interface

        - network interface of VM

                - before start vm, you can set serval network interface (without name like eht0)

                - when vm is started
                /etc/udev/rules.d/70-persistent-net.rules is used to do some mapping
                between your defined interface without name and runtime interface by its name, like eht0, eth1 (check ifconfig)
                you can modify or delete it, need to reboot

                - interface setting with name is in file like /etc/sysconfig/network-scripts/ifcfg-eth0
                
                - usually when have issue, you need to check below stuff
                ifconfig
                ls /etc/sysconfig/network-scripts/
                cat /etc/sysconfig/network-scripts/ifcfg-eth0
                cat /etc/udev/rules.d/70-persistent-net.rules
                rm /etc/udev/rules.d/70-persistent-net.rules
                service network restart
                service network restart
                service NetworkManager stop

        - example

                TYPE=Ethernet
                BOOTPROTO=none
                IPADDR=10.10.10.110
                PREFIX=24
                GATEWAY=10.10.10.111
                DEFROUTE=yes
                IPV4_FAILURE_FATAL=yes
                IPV6INIT=no
                NAME=eth0
                UUID=86d44060-4579-48cc-b85b-219a206ca37c
                ONBOOT=yes
                HWADDR=00:50:56:95:09:76
                LAST_CONNECT=1411004329

- OSI 7 model

- encoding

        - ascii
        1 byte character encoding which is limited to 128 characters

        - unicode vs utf8
        https://stackoverflow.com/questions/3951722/whats-the-difference-between-unicode-and-utf-8

        Unicode is a character set used to translate characters into numbers.
        UTF-8 (Unicode Transformation Format) is an variable length encoding format (using 1 to 4 bytes) used to translate numbers into binary data. 

        1 byte for 128 US-ASCII characters
        2 bytes for the next 1920 characters which covers the reminder of almost all latin.
        3 bytes for chinese/japanese/korean.
        4 bytes for CJK characters/historic scripts/math symbols/emoji

        e.g. 
        character set:
        code point (fake)	1	2	3
        character	        a	b	c

        if you want to store abc, utf8 transform 123 to binary 00000001 00000010 00000100
        if you want to read what the binary is, transform it to 123 and by comparing the character set you get abc.
        if you encode content with utf8, but decode with other format like GBK, you will get strange characters because it may not read 8 bits for each character.

        - java
        string is utf16 encoding by default.
        string is array of char, 1 char = 2 bytes.

        - golang
        https://blog.golang.org/strings

        Source code in Go is defined to be UTF-8 text; no other representation is allowed.
        so string literals are UTF-8.
        string is array of byte, when you use range over grammer for a string, runes are extracted out from the byte array, 1 rune = 4 bytes.


