# Unidad 1
---
# IPv4
```
do sh ip route
```
- SW: Switch
- R1: Router 1
### Comandos basicos
mirar la configuracion del equipo
```
en
sh run
```
Ingreso a configuracion de terminal.
```
en
config t
```
Nombre del equipo anfitrion (por ejemplo un switch).
```
hostname SW-1
```
Acceder a una interfaz (puerto de conexion) por ejemplo vlan 1 de un switch, asignarle una **IPv4** y encender al puerto interfaz.
- Red: 192.168.100.0/24
```
int vlan 1
ip add 192.168.100.254 255.255.255.0
no shutdown
```
hacer ping a una direccion
```
en
config t
do ping 192.168.100.3
```

### Si se desea conectar 2 o mas switches entre si, se le asigan ipv4 a cada uno con distintas redes mediante los comandos anteriores

# Ruteo
Configurar el reloj si da error
```
clock rate 2000000
```
### Default-Gateway
IP de R1: 192.168.100.254 
SW CLI:
```
en
config t
ip default-gateway 192.168.100.254
```

## Asignacion de direcciones ip a routers con diferentes redes
- R1:
	- Gi1 192.168.100.0/24
	- Gi2 148.208.144.0/23
	- Se0 10.0.0.1/30
- R2:
	- Gi1 172.16.100.0/24
	- Gi2 200.34.128.0/24
	- Se0 10.0.0.2/30

Agregar una ruta específica a la tabla de enrutamiento del dispositivo 
- R1 CLI:
```
en
config t
ip route 172.16.100.0 255.255.255.0 10.0.0.2
ip route 200.34.128.0 255.255.255.0 10.0.0.2
```
- R2 CLI:
```
en
config t
ip route 192.168.100.0 255.255.255.0 10.0.0.1
ip route 148.208.144.0 255.255.254.0 10.0.0.1
```
### configurar una ruta estática predeterminada
forma de localizar dispositivos sin espesificar su ruta 
- R1 CLI:
```
en
config t
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```
- R2 CLI:
```
en
config t
ip route 0.0.0.0 0.0.0.0 10.0.0.1
```
---
# IPv6
```
do sh ipv6 route
```
lo primero se configura en R1 para que se puedan asignar direcciones fijas o dinamicas EUI64
```
en
config t
ipv6 unicast-routing
```
luego ya podemos asignar
```
int gi 0/0/0
ipv6 add add 2020:db8:acad:1::100/64
ipv6 add fe80::1 link-local
no shut
```
- Los SW no se configuran con ipv6, son capa 2, solo manejan direcciones MAC

- Con IPV6 se puden asignar IPs automaticamente sin necesitar DHCP usando el router usando el link-local y su red ipv6

- Se pueden asigar redes IPv4 e IPv6 a una interfaz al mismo tiempo

## Ruteo IPv6
- R1:
	- Gi0 2001:DB8:1:1::1/64
	- Gi0 FE80::1 link-local
	- Se0 2001:DB8:1:A001::1/64
	- Se0 FE80::1 link-local
- R2:
	- Gi0 2001:DB8:1:1::1/64
	- Gi0 FE80::1 link-local
	- Se0 2001:DB8:1:A001::1/64
	- Se0 FE80::1 link-local

Asignacion de ruteo IPv6

- R1 CLI:
```
en
config t
ipv6 route 2001:DB8:1:2::/64 2001:DB8:1:A001::2
```
- R2 CLI:
```
en
config t
ipv6 route 2001:DB8:1:1::/64 2001:DB8:1:A001::1
```
### configurar una ruta estática predeterminada
- R1 CLI:
```
en
config t
ipv6 route ::/0 2001:DB8:1:A001::2
```
- R2 CLI:
```
en
config t
ipv6 route ::/0 2001:DB8:1:A001::1
```
---
# Ruteo dinámico IPv4-6
configuración del protocolo de enrutamiento RIP (Routing Information Protocol)
```
en
config t
router rip
network 10.10.10.0
network 192.168.20.0
... 
``` 

