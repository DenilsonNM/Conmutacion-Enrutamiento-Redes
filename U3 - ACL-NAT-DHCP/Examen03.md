# EXAMEN 03

## Matriz

```
en
conf t
hostname Matriz
ipv6 unicast-r

int se0/0/0
ip add 10.10.0.2 255.255.255.252
ipv6 add 2010:DB8:ACAD:1::2/64
ipv6 add fe80::1 link-local

int gi0/1
ip add 200.34.128.2 255.255.255.252
ipv6 add 2000:acad:cafe:F::1/127
ipv6 address FE80::1 link-local
no sh

int gi0/0
ip add 20.10.0.2 255.255.255.252
ipv6 add 2020:DB8:ACAD:1::2/64
ipv6 add fe80::1 link-local
no sh

int gi0/1/0
ip add 30.10.0.2 255.255.255.252
no sh

ip route 0.0.0.0 0.0.0.0 10.10.0.1
ipv6 route ::/0 2010:DB8:ACAD:1::1

ip route 0.0.0.0 0.0.0.0 200.34.128.1
ipv6 route ::/0 2000:acad:cafe:F::

ip route 0.0.0.0 0.0.0.0 20.10.0.1
ipv6 route ::/0 2020:DB8:ACAD:1::1

ip route 0.0.0.0 0.0.0.0 30.10.0.1
```
-------------------------------------
# NORTE

![](/images/examen1.png)

## RT-IPv6

```
en
conf t
hostname RT-IPv6
ipv6 unicast-r

int gi0/0
ip add 10.0.0.2 255.255.255.252
ipv6 add 2010:DB8:ACAD:2::100/64
ipv6 add fe80::1 link-local
no sh
ipv6 dhcp server NORTE
ipv6 nd managed-config-flag

int se0/1/0
ip add 10.10.0.1 255.255.255.252
ipv6 add 2010:DB8:ACAD:1::1/64
ipv6 add fe80::1 link-local
no sh

ipv6 dhcp pool NORTE
add pref 2010:DB8:ACAD:2::/64
dns-server 2000:DB8:ACAD:FE0::1
domain-name norte.com

ip route 0.0.0.0 0.0.0.0 10.10.0.2
ipv6 route ::/0 2010:DB8:ACAD:1::2
```

## SW-IPv6

```
en
conf t
hostname SW-IPv6
int vlan 1
ip add 10.0.0.1 255.255.255.252
no sh

int gi0/1-2
sw mo tr
no sh

```

-------------------------------------
# CENTRO

![](/images/examen2.png)

## RT-IPv46

```
en
conf t
hostname RT-IPv46
ipv6 unicast-r

int gi0/0/0
ip add 20.10.0.1 255.255.255.252
ipv6 add 2020:DB8:ACAD:1::1/64
ipv6 add fe80::1 link-local
no sh

int gi0/0/1
ip add 20.0.0.2 255.255.255.252
no sh

int gi0/0/1.10
encap dot1q 10
ip add 192.168.100.254 255.255.255.0
ipv6 add 2020:DB8:ACAD:2::100/64
ipv6 add fe80::1 link-local
ipv6 dhcp server CEN10-2
ipv6 nd other-config-flag

int gi0/0/1.20
encap dot1q 20
ip add 192.168.150.254 255.255.255.0

ip dhcp excluded-address 192.168.100.254
ip dhcp excluded-address 192.168.150.254

ip dhcp pool CEN10
network 192.168.100.0 255.255.255.0
default-router  192.168.100.254
dns-server 200.23.57.1
domain-name centro.com

ipv6 dhcp pool CEN10-2
dns-server 2000:db8:acad:fe0::1
domain-name centro.com

ip dhcp pool CEN20
network 192.168.150.0 255.255.255.0
default-router  192.168.150.254
dns-server 200.23.57.1
domain-name centro.com

ip route 0.0.0.0 0.0.0.0 20.10.0.2
ipv6 route ::/0 2020:DB8:ACAD:1::2

```

## SW-IPv46

```
en
conf t
hostname SW-IPv46

int vlan 1
ip add 20.0.0.1 255.255.255.252
no sh

vlan 10
name Direccion
int range fa0/1-5
sw mo acc
sw acc vlan 10
vlan 20
name Empleados
int range fa0/6-10
sw mo acc
sw acc vlan 20
int range fa0/11-24
sh

int range gi0/1-2
sw mo tr
```
-------------------------------------
# SUR

![](/images/examen3.png)

## RT-IPv4

```
en
conf t
hostname RT-IPv4

int gi0/1/0
ip add 30.10.0.1 255.255.255.252
no sh

int gi0/0
ip add 30.0.0.2 255.255.255.252
no sh

int gi0/0.10
encap dot1q 10
ip add 192.168.200.254 255.255.255.0

int gi0/0.20
encap dot1q 20
ip add 192.168.250.254 255.255.255.0

ip dhcp excluded-address 192.168.200.254
ip dhcp excluded-address 192.168.250.254

ip dhcp pool SUR10
network 192.168.200.0 255.255.255.0
default-router  192.168.200.254
dns-server 200.23.57.1
domain-name sur.com

ip dhcp pool SUR20
network 192.168.250.0 255.255.255.0
default-router  192.168.250.254
dns-server 200.23.57.1
domain-name sur.com

ip route 0.0.0.0 0.0.0.0 30.10.0.2
```
## SW-IPv4

```
en
conf t
hostname SW-IPv4

int vlan 1
ip add 30.0.0.1 255.255.255.252
no sh

vlan 10
name Ventas
int range fa0/1-5
sw mo acc
sw acc vlan 10
vlan 20
name Compras
int range fa0/6-10
sw mo acc
sw acc vlan 20
int range fa0/11-24
sh

int range gi0/1-2
sw mo tr
```
-------------------------------------
# ISP --> MATRIZ

![](/images/examen4.png)

## ISP

```
int gi0/0/0
ipv6 address 2000:ACAD:CAFE:F::/127
ip route 0.0.0.0 0.0.0.0 200.34.128.2
sh

ipv6 route ::/0 2000:acad:cafe:F::1
```