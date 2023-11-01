vm2:
network:
  ethernets:
    enp0s8:     #NAT 
      dhcp4: yes
    enp0s3:     #Host-Only
      dhcp4: no
      addresses: 
        - 192.168.56.3/24
      nameservers:
        addresses: 
          - 8.8.8.8
  version: 2


vm3:
network:
  ethernets:
    enp0s3:     #Host-Only      
      dhcp4: no
      addresses: 
        - 192.168.56.4/24
      gateway4: 192.168.56.3
      nameservers:
        addresses:
          - 8.8.8.8
  version: 2
