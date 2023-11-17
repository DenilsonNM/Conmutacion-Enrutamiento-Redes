# Unidad 3
---
# ACL

```
show access-lists
show ip interface
```
Listas de control de acceso, controlan el flujo de tráfico basándose en reglas específicas

- ACL de entrada: filtran paquetes que ingresan a una interfaz, antes de que se enruten a la interfaz de salida
- ACL de salida: filtran paquetes despues del enrutamiento, independiente de la interfaz de entrada
- ACL por protocolo (ipv4 o ipv6), interfaz (ej. gi0/0), sentido (entrada y salida)
- ACL extendidas: se colocan cerca del origne
- ACL estandar: se colocan cerca del destino

### Eliminar ACL

Por ejemplo un ACL con numero 11

```
en
conf t
int se0/0/0
no ip access-group 11 out
exit
no access-list 11
```

## ACL estandar

```
en
config t
access-list 1 deny 192.168.11.0 0.0.0.255
access-l 1 permit any
int gi0/0
ip access-group 1 out
do sh ip int gi0/0
```
- Niega el tráfico desde la red 192.168.11.0/24 y se permite cualquier otro tráfico saliente en la interfaz GigabitEthernet0/0
- `access-list 1 deny 192.168.11.0` creando una ACL con el numero 1, y niega el acceso a la red 192.168.11.0
- `access-l 1 permit any` para permitir el resto del tráfico, de manera predeterminada, ACL deniegan todo el tráfico que no coincide con ninguna regla
- `ip access-g 1 out` asignar la ACL 1 a la interfaz para filtrar el trafico saliente

```
en
config t
access-list 1 permit 192.168.11.0 0.0.0.255
access-l 1 deny any
int gi0/0
ip access-g 1 out
```
- Permite el tráfico desde la red 192.168.11.0/24 y se niega cualquier otro tráfico saliente en la interfaz GigabitEthernet0/0
- ACLs implícitamente deniegan el tráfico que no coincide con ninguna regla, es rededundante poner `access-l 1 deny any`

```
en
config t
line vty 0 15
transport input ssh
access-class 21 in
exit
access-l 21 permit 192.168.10.0 0.0.0.255
access-l 21 deny any
```
- para las lineas vty se usa `access-class [numero] out/in` no admite acl con nombre

## ACL estándar con nombre

```
en
config t
ip access-list standard ejemplo1
deny host 192.168.20.4
permit any
int gi0/0
ip access-g ejemplo1 out
```

---
# DHCP

### Exclusion de direcciones

```
ip dhcp excluded-address 10.32.100.253 10.32.100.254
```
- excluye las direcciones asignadas a los esquipos SW y al R1 por ejemplo

```
ip dhcp excluded-address 10.32.100.1 10.32.100.9
```
- exluye direcciones de 1 al 9, para que la asignacion empiece a partir de la direccion 10

### POOL de DHCPv4

![](/images/dhcp1.png)

![](/images/dhcp2.png)


```
ip dhcp pool Mi-primer-DHCP
network 10.32.100.0 255.255.255.0
default-router 10.32.100.254
dns-server 192.168.11.5 *
domain-name ejemplo.com
end
```
- `network 10.32.100.0 255.255.255.0` es la red que repartira ips a los dispositivos
- `default-router 10.32.100.254` router que actuará como puerta de enlace predeterminada para los dispositivos que obtienen direcciones IP de este pool
- `dns-server 192.168.11.5` dirección IP del servidor DNS que se proporcionará a los dispositivos clientes DHCP, si no hay se omite poner
- `domain-name ejemplo.com` nombre de dominio que se asignará a los dispositivos clientes DHCP, no confundir con `ip domain-name` en la configuracion de terminal del dispositivo

### Si existe particiones VLAN en el router

```
int gi0/0/0.20
encap dot1q 20
ip add 200.34.128.254 255.255.255.0
```
se crea un pool por cada vlan (ej. de la 20)

```
ip dhcp pool VLAN20
network 200.34.128.0 255.255.255.0
default-router 200.34.128.254
domain-n vlan20.com
```
- no olvidar asignar una ip a la interfaz sin particion vlan jusnto con el SW para que se comuniquen en red

### Router como cliente DHCP

```
int gi0/1
ip address dhcp
no sh
```
- `ip address dhcp` para obtener su dirección IP automáticamente del servidor DHCP

### IP helper

```
int gi0/1
ip helper-address 10.1.1.2
``` 


