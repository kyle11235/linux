# fix eth0 for cloned vm (failed !!!!!!!!!!!!!!)

        refering to vmware case:
        https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2002767

        issue is cloned vm, has no option to select from network setting icon, and eth0 ip disappears

        1. let's refresh mac address
        shutdown vm, refresh mac address from virtualbox setting, and note 08 00 27 39 60 C3

        2. open vm, eth0 will disappear, and eth1 will show up if you check with ifconfig
        vi /etc/sysconfig/network-scripts/ifcfg-eth0 to use new mac address

        3. vi or just delete below mapping rule file
        vi /etc/udev/rules.d/70-persistent-net.rules
        line1 is for old eth0 with old mac address,
        line2 is for new eth1 with new mac address,
        delete old line1, and update new line2's name to eth0

        4. reboot, you should see eth0 with ifconfig

        5. but still no ip address in eth0

        6. also, still no option from network setting icon

        7. then try re-installing guest additions module, does not work

        8. disable dhcp

        DEVICE=eth0
        ONBOOT=yes
        NM_CONTROLLED=yes          -> no will not cause below error, but i need the NetworkManager 
        BOOTPROTO=none
        IPADDR=10.0.2.15
        NETMASK=255.255.255.0
        GATEWAY=10.0.2.2
        DNS1=8.8.8.8
        NAME="System eth0"
        HWADDR=08:00:27:39:60:C3


        /etc/init.d/network restart


        Error: connection activation failed: Device not managed by	NetworkManager or unavailable
