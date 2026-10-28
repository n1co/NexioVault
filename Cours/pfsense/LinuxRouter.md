https://medium.com/@lfoster49203/setting-up-ubuntu-as-a-router-with-advanced-routing-features-4511abc5e1eb

https://us.informatiweb-pro.net/system-admin/linux/debian-transform-your-server-into-a-router-and-a-dhcp-server.html



Pas internet:


|     |                      |
| --- | -------------------- |
| 1   | `vi` `/etc/rc.local` |

And add this before the "exit" line.

|            |                                                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------------------------------- |
| 1<br><br>2 | `/sbin/iptables` `-P FORWARD ACCEPT`<br><br>`/sbin/iptables` `--table nat -A POSTROUTING -o enp0s3 -j MASQUERADE` |

echo "200 custom_table" >> /etc/iproute2/rt_tables
   65  ip rule add from 192.168.1.10 table custom_table
   66  ip route
   67  ip route add default via 10.0.2.2 dev eth0 table custom_table
   68  ip route add default via 10.0.2.2 dev enp0s3 table custom_table
   69  iptables -P FORWARD ACCEPT
   70  iptables --table nat -A POSTROUTING -o enp0s3 -j MASQUERADE