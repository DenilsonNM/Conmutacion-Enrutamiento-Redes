# DHCP
## Datos
- tienen tiempo disponible de vida (caducidad)
- el router no pasa trafico de bloadcast, por eso no va a pasar una direccion ip a otro extremo con otro router, a menos que se configure
- el trabajo de router no es asignar ips, es el servidor, pero el router tambien puede

## comandos
### exclucion
```
//para poner un rango, entonces su primera direccion sera la 10
ip dhcp excluded-addres 192.168.10.1 192.168.10.9
//para poner solo una
ip dhcp excluded-addres 192.168.10.254
```

### configurar un POOL
```
conf t
ip dhcp pool LAN-POOL-1
network 192.168.10.0 255.255.255.0
//direccion del enrutador
default-router 192.168.10.1
//el dns esta en otra red
dns-server 192.168.11.5
//se usa lo mimso para ssh
domain-name example.com
end
...
w
```
### se puede desabilitar
```
no service dhcp
```
### se puede poner limite de duracion
```
lease {days [hours] [minutes] | infinite}
```
## si se tiene un servidor DHCP en lugar de un router
1. el servidor tiene la ip 192.168.11.6
2. en el router poner
```
ip helper-address 192.168.11.6
```
# DHCP IPV6

## opcion de SLAAC
### ipv6 managed-config-flag
- poner direcciones ipv6 espesificas de modo dinamico a las pc
### ipv6 nd other-config-flag
- pener DNS, dominio y datos adicionales

por defecto cisco trae estas 2 banderas apagadas

# NAT estatica
148.208.144.1-5
192.108.0.0

ip nat pool NAT-POOL 148.208.144.1 148.208.144.5
access-list 1 permit 192.108.0.0 0.0.255.255
ip nat inside source-list 1 pool NAT-POOL
exit
int gi0/0
ip nat inside 
int gi0/1


# PAT
agarrar una direccion de red y asignarle un numero dinamico de puerto
una ip para varias
ip nat inside source-list 1 pool NAT-POOL overlord

# unidad 3 conmutación y redes

# ACL - limitación de acceso a redes

## tarea 1
### checar si existe access list y cual es
- sh access-l
- sh run
### quitar ACL a una int y en general
- int gi0/0
- no ip access-group 11 out
- exit
- no access-l 11
#### verificar con `ping` en pc y `sh r`

## tarea 2

### crear un ACL para el router r2 y r3
- access-l 1 deny 192.168.11.0 0.0.0.255
### crear otra regla para la ACL 1
- access-l 1 permit any
- int gi0/0
- ip access-g 1 out
#### verificar con: `sh r`

## tarea 3
### checar las conexiones
- ping
### configurar el ACL con nombre en R1
- ip access-l s File_Server_Restrictions
- permit host 192.168.20.4
- deny any
### aplicar a la pc int 0/1/0
- ip access-g File_Server_Restrictions
- exit
- w