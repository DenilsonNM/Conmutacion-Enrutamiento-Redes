# Unidad 2
---
# Seguridad en Switches

## Seguridad basica

- Contraseña de acceso a la consola: Cisco
- Contraseña de acceso a modo privilegiado: Class

```
en
config t
enable password class *
service password-encryption
line con 0
password cisco
login
```
- Es mas seguro usar `enable secret class` que `enable password class`

## SSH

Estableciendo un nombre de dominio, generando claves criptográficas RSA y creando un nombre de usuario con una contraseña para propósitos de autenticación

```
en
conf t
ip domain-name cisco.com
crypto key generate rsa
username admin priv 15 secret cisco *
```
- Tambien se puede usar `username admin priv 15 secret cisco`. El nivel de privilegio 15 es el nivel máximo de privilegios en un dispositivo Cisco (modo privilegiado o enable mode). `username admin secret cisco` por defecto, el nivel de privilegio será 1, que es un nivel de privilegio estándar sin acceso completo al modo privilegiado 
- Al ingresar `generate rsa` te pide cuantos bits irán en el módulo, defaul 512, generalmente usamos 1024

```
en
conf t
line vty 0 15
transport input ssh
login local
exit
ip ssh version 2
```
- `transport input ssh` deshabilita el acceso Telnet y solo permite conexiones SSH
- `login local` la autenticación se realizará mediante la base de datos de usuarios locales configurada en el dispositivo
- `ip ssh version 2` usa la versión 2 del protocolo SSH. SSHv2 es más seguro

## Acceder por ssh desde PC

usando la ip del SW

- PC1:
```
ssh -l admin 10.10.10.2
```

## Seguridad en puertos

- Por ejemplo el puerto fa0/2 de un SW

```
en
conf t
int fa 0/2
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
do show port-security fa0/2
```
- `switchport mode access` interfaz de acceso. la interfaz está destinada a conectarse a un único dispositivo final, host o servidor
- `switchport port-security` Habilita la funcionalidad de seguridad de puerto
- `switchport port-security maximum 1` Establece el número máximo de direcciones MAC permitidas en el puerto a una
- `switchport port-security mac-address sticky` la interfaz "aprenda" automáticamente la dirección MAC del dispositivo que se conecta y la adhiera a la configuración de seguridad de puerto
- `switchport port-security violation shutdown` la interfaz se apagará si se detecta una violación de seguridad (shutsown, protect, restrict)

![](/images/seguridadpuertos.png)

### Asignar direcciones MAC espesificas

- PC1 MAC = 00E0.B027.2245
- SW:
```
int fa0/1
switchport port-security mac-address sticky 00E0.B027.2245
```

### Deshabilitar puertos no usados

Por ejemplo los puertos del SW 20 al 24

```
en
conf t
int range fa0/20-24
shutdown
```

### Mensaje
se muestra a los usuarios cuando se conectan al dispositivo

```
en
conf t
banner motd Bienvenido
```
---
# VLAN

### Crear particiones VLANS en un SW y con un nombre

```
en
conf t
vlan 10
name ejemplo1
```
Asignarle a uno o varios puertos a la vlan creada

- SW:
```
int range fa0/1-10
switchport mode access
switchport access vlan 10
```
configurando una subinterface

- R1:
```
int gi0/0/0.10
encap dot1q 10
ip add 200.23.57.254 255.255.255.0
```
### Creando una vlan nativa

- SW:
```
vlan 90
name nativa *
int range gi0/1-2
switchport mode trunk
switchport trunk native vlan 90
int vlan 90
ip add 10.10.10.253 255.255.255.0
```
- R1:
conectado al SW1 por gi0/0/0
```
int gi0/0/0.90
encap dot1q 90 native
ip add 10.10.10.254 255.255.255.0
int gi0/0/0
no sh
```
- en `IPv6` aparte de la direccion, tambien necesita su link-local, `ipv6 add 2001:db8:acad:cafe::ff/64` y `ipv6 add fe80::10 link-local` por ejemplo





