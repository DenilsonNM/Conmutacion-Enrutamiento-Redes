# Asignacion de ip y contraseña switch/router
## Comandos:
```
en
config t
hostname
enable password Cisco
service password-encryption
line con 0
password Class
login
service password-encryption
int vlan 1 o GigabitEthernet0/0/0
ip add 200.23.57.254 255.255.255.128
no shut
```

## Actividad 3
```
ip add 172.16.100.254 255.255.255.0
```
```
ip add 200.34.128.253 255.255.255.0
```
```
ip default-gateway 192.168.100.254
ip default-gateway 148.208.145.253
ip default-gateway 172.16.100.253
ip default-gateway 200.34.128.253
```

## Comandos para conectar 2 router para que lleguen de redes diferentes

### levantar interfaces:
Norte:
```
en
config t
int serial 0/1/0
ip add 10.0.0.1 255.255.255.252
no shut
```
Sur:
```
en
config t
int serial 0/1/0
ip add 10.0.0.2 255.255.255.252
no shut
```
```
do ping 10.0.0.2
```
Norte:
(poner las redes que no conosco)
```
ip route 172.16.100.0 255.255.255.0 10.0.0.2
ip route 200.34.128.0 255.255.255.0 10.0.0.2
```
Sur:
```
ip route 192.168.100.0 255.255.255.0 10.0.0.1
ip route 148.208.144.0 255.255.254.0 10.0.0.1
```
### Mejor poner
```
ip route 0.0.0.0 0.0.0.0 10.0.0.2
ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

Ej: R1
```
ip route 0.0.0.0 0.0.0.0 172.31.1.193
ip default-g 172.16.33.253
```