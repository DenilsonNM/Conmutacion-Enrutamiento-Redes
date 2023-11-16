# Unidad 2
---
# IPv4
```
en
conf t
```
---
# IPv6
```
en
conf t
```
---
# IPv4-6
### SSH
Estableciendo un nombre de dominio, generando claves criptográficas RSA y creando un nombre de usuario con una contraseña para propósitos de autenticación
```
en
conf t
ip domain-name cisco.com
crypto key generate rsa
username admin secret ccna
```
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

### Deshabilitar puertos no usados
Por ejemplo los puertos del SW 20 al 24
```
en
conf t
int range fa0/20-24
shutdown
```
### Seguridad en puertos
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
show port-security fa0/2
```
- `switchport mode access` interfaz de acceso. la interfaz está destinada a conectarse a un único dispositivo final, host o servidor
- `switchport port-security` Habilita la funcionalidad de seguridad de puerto
- `switchport port-security maximum 1` Establece el número máximo de direcciones MAC permitidas en el puerto a una
- `switchport port-security mac-address sticky` la interfaz "aprenda" automáticamente la dirección MAC del dispositivo que se conecta y la adhiera a la configuración de seguridad de puerto
- `switchport port-security violation shutdown` la interfaz se apagará si se detecta una violación de seguridad (shutsown, protect, restrict)

![](/images/seguridadpuertos.png)







