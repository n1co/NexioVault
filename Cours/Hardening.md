### SSH
* Horaires de connexion
* Deconnexion inactive

### HTTPD
* Partition chiffrée



```shell
ip link set enp0s3 up
ip address add 10.0.2.15/24 broadcast + dev enp0s3
ip route show
ip route add 0.0.0.0/0 via 10.0.1.1 dev enp0s3
echo "nameserver 1.1.1.1" >> /etc/resolv.conf


#LUKS
pacman -S lvm2

```

