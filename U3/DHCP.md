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