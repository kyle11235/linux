

- virtualbox

        https://www.virtualbox.org/manual/ch06.html#network_nat_service

        - NAT (Network Address Translation)

                easy to have basic network to visit internet
                like private <-> NAT <-> public
                vm receives its network address and configuration on the private network from a DHCP server integrated into Oracle VM VirtualBox
                network for 1st cart is 10.0.2.0, network for 2nd card of 2nd vm is 10.0.3.0

                - from guest to visit external network
                1.in office, wifi ok
                2.in office, cable needs proxy probably
                3.at home, wifi ok

                - from host to guest
                1.port forwarding
        
                - from guest to visit host
                check ip from host
                1.try to use the local connection IPV4
                2.try default mask

        - NAT network

                VMs talk to each other
                host port forward to VMs

                - steps
                1. preference -> network -> add nat network, default 10.0.2.0/24
                2. change network of different VMs to NAT network, select the created one
                3. VMs get different IPs, able to ping each other

        - host-only networking

                host + VMs, using virtual network interface

        - bridged networking

                This is for more advanced networking needs, such as network simulations and running servers in a guest. 
                When enabled, Oracle VM VirtualBox connects to one of your installed network cards and exchanges network packets directly

                With bridged networking, Oracle VM VirtualBox uses a host driver to intercept data from the physical network and inject data into it, effectively creating a new network interface in software. 
                
                When a guest is using such a new software interface, it looks to the host system as though the guest were physically connected to the interface using a network cable. The host can send data to the guest through that interface and receive data from it. This means that you can set up routing or bridging between the guest and the rest of your network.


- different networking modes Virtualbox provides

        Virtualbox NAT gives each guest that uses it an independent channel through your host PC to the internet, so the default IP address in each channel will be the same. NAT behaves the same way your house router works. You have a public IP address, provided by your internet company, which identifies your house on the internet. Inside your house the router uses NAT to give your PCs private IP addresses, like 192.168.1.whatever. Your neighbor may have exactly the same setup, and his PCs may also have 192.168.1.whatever IP addresses, and everything will work, because the public IP address for your and your neighbor's houses are different.

        It sounds like you want these guests to all be on the same network. See the Virtualbox manual, section 6, on the different networking modes Virtualbox provides.

        If you want the guests to be in their own private network with no contact to the host or the outside world, use Internal networking, and set all the guests to the same Internal network name. You will need to set static IP addresses in each guest OS, or use the manual's instructions to add a DHCP server to the Internal network (command line instructions, btw).

        If you also want the host PC to talk with the guests, use Host-Only networking. Same as Internal, but the host is in on the network, too, and there's an automatic DHCP server to hand out IP addresses. You can still set static IP addresses if you want, just use the Host-Only network's address range.

        If you also want the other PCs in your house network and the host PC to talk to the guests, you'll need Bridged. As Bill said, you'll need a network router handing out IP addresses for Bridged to work right away, or set static IP addresses for your guests in the same range that the host uses. (Note that if your host PC is directly connected to the internet without a router between, Bridged will not work, as Bill mentioned. In this case, Host-only or Internal are your choices. Or buy a router.) One other caveat about Bridged, it does not always work with Wi-Fi adapters due to poorly-written Wi-Fi adapter drivers or Wi-Fi access point firmware. It's a crap-shoot whether yours will work or not, just have to try it.

        There is one more kind of network, "NAT network", which is like a virtual router just for the guests attached to it. All the guests will get compatible IP addresses to communicate with each other, and there is a path to the internet, but the host and other physical PCs can't get in.

