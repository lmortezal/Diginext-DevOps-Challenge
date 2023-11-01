sudo iptables -t nat -A POSTROUTING -o enp0s8 -j MASQUERADE

sudo iptables-save > /etc/iptables/rules.v4