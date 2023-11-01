I used a virtual‌box in this task and operated on the Ubuntu operating system, version 22.

I assigned two network adapters to Machine 2, including NAT and Host-Only, and allocated only a Host-Only adapter to Machine 3 (Image 1 , 2).

Because there was no DHCP server in the Host-Only, and we weren't asked to set up servers manually, we assigned IP addresses manually using netplan. This ensures that the configurations persist even after a reboot (netplan.md).

Now that two virtual machines can see each other and the gateway of the machine without internet is set to the address of the other machine, we need to adjust the firewall settings on the second machine to enable internet access.
1. Enable IP Forwarding :
When IP forwarding is enabled (net.ipv4.ip_forward=1), it allows the Linux kernel to forward packets from one network interface to another.
I modified the sysctl.conf file for this part so that the changes persist after a reboot. However, it was also possible to enable it immediately using the command "sysctl -w net.ipv4.ip_forward=1".
2. Enable NAT :
NAT is essential for servers that are not directly connected to the internet. When Server B sends a packet to the internet, Server A changes the source address of the packet to its own address. When the response comes back, Server A translates the destination address back to Server B's address.
At this stage, I used iptables, and to ensure that the rules persist after each reboot, I installed a package called "iptables-persistent." With this package, you can save the rules in the configuration file, ensuring they are retained even after a reboot. (Iptables.md and result-1.jpg)

For the fifth part of the task, I used SSH and a proxy chain, but there are various methods available for accomplishing this.
I connected to my server in Germany using the command "ssh -D 1080 root@german," created a port in my local machine, and then added two lines to the proxychain configuration to connect through the proxy. From now on, any command using proxychain will be routed through the German server. (proxychain.md and result-2.jpg)
