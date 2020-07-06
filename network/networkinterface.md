- guide

        https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/ch-networkscripts.html

- Network Configuration Files

        /etc/hosts
        The main purpose of this file is to resolve hostnames that cannot be resolved any other way. It can also be used to resolve hostnames on small networks with no DNS server. Regardless of the type of network the computer is on, this file should contain a line specifying the IP address of the loopback device (127.0.0.1) as localhost.localdomain. For more information, refer to the hosts man page.

        /etc/resolv.conf
        This file specifies the IP addresses of DNS servers and the search domain. Unless configured to do otherwise, the network initialization scripts populate this file. For more information about this file, refer to the resolv.conf man page.

        /etc/sysconfig/network
        This file specifies routing and host information for all network interfaces. For more information about this file and the directives it accepts, refer to Section 27.1.22, “/etc/sysconfig/network”.

        /etc/sysconfig/network-scripts/ifcfg-<interface-name>
        For each network interface, there is a corresponding interface configuration script. Each of these files provide information specific to a particular network interface. Refer to Section 13.2, “Interface Configuration Files” for more information on this type of file and the directives it accepts

- network interface

        Under Red Hat Enterprise Linux, all network communications occur between configured software interfaces and physical networking devices connected to the system.

        The configuration files for network interfaces are located in the /etc/sysconfig/network-scripts/ directory. The scripts used to activate and deactivate these network interfaces are also located here. Although the number and type of interface files can differ from system to system, there are three categories of files that exist in this directory:

        - Interface configuration files
        - Interface control scripts
        - Network function files

        The files in each of these categories work together to enable various network devices.
        This chapter explores the relationship between these files and how they are used.

- Interface configuration files

        Interface configuration files control the software interfaces for individual network devices. As the system boots, it uses these files to determine what interfaces to bring up and how to configure them. These files are usually named ifcfg-<name>, where <name> refers to the name of the device that the configuration file controls

        - Ethernet Interfaces
        One of the most common interface files is ifcfg-eth0, which controls the first Ethernet network interface card or NIC in the system. In a system with multiple NICs, there are multiple ifcfg-eth<X> files (where <X> is a unique number corresponding to a specific interface). Because each device has its own configuration file, an administrator can control how each interface functions individually.

        The following is a sample ifcfg-eth0 file for a system using a fixed IP address:

        DEVICE=eth0 
        BOOTPROTO=none 
        ONBOOT=yes 
        NETWORK=10.0.1.0 
        NETMASK=255.255.255.0 
        IPADDR=10.0.1.27 
        USERCTL=no

        - IPsec Interfaces
        The following example shows the ifcfg file for a network-to-network IPsec connection for LAN A. The unique name to identify the connection in this example is ipsec1, so the resulting file is named /etc/sysconfig/network-scripts/ifcfg-ipsec1.

        TYPE=IPsec 
        ONBOOT=yes 
        IKE_METHOD=PSK 
        SRCNET=192.168.1.0/24 
        DSTNET=192.168.2.0/24 
        DST=X.X.X.X
        In the example above, X.X.X.X is the publicly routable IP address of the destination IPsec router
                
        - ...

- Interface control scripts

        ifup eth0
        ifdown eth0

        The easiest way to manipulate all network scripts simultaneously 
        e.g.
        /sbin/service network status
        /sbin/service network start/stop/restart

- Network function files

        The /etc/sysconfig/network-scripts/network-functions file contains the most commonly used IPv4 functions, which are useful to many interface control scripts. These functions include contacting running programs that have requested information about changes in the status of an interface, setting hostnames, finding a gateway device, verifying whether or not a particular device is down, and adding a default route

