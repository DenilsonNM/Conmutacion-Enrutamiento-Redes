# IPV4

## Comandos basicos
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
Acceder a una interfaz (puerto de conexion) por ejemplo vlan 1 de un switch, asignarle una **IPv4** y encender el puerto interfaz.
- Red: 192.168.100.0/24
```
int vlan 1
ip add 192.168.100.254 255.255.255.0
no shutdown
```
### Si se desea conectar 2 o mas switches entre si se le asigan ipv4 a cada uno con distintas redes mediante los comandos anteriores