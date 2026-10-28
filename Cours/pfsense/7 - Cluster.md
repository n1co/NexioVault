https://provya.net/?d=2016/10/02/07/48/16-pfsense-configurer-un-cluster-de-2-pfsense-redondants-failover

https://www.provya.net/?d=2019/11/05/10/02/58-pfsense-tout-comprendre-aux-alias

Mise en place d'un cluster de 2 pfsense redondants (failover)


pfSenseA - WAN : 172.25.46.101 - 192.168.0.4
pfSenseB - WAN : 172.25.46.102 - 192.168.0.5
@IP virtuelle - WAN : 172.25.46.100 - 192.168.0.100

pfSenseA - LAN : 192.168.0.11 - 192.168.56.101
pfSenseB - LAN : 192.168.0.12 - 192.168.56.102
@IP virtuelle LAN : 192.168.0.10 - 192.168.56.100

