# Comandos del switch
```
#ENABLE = EN = para entrar al modo avanzado
#conf t = CONFIGURE TERMINAL
#hostname SW-1
#enable password Cisco = contraseña
#sh running = show running
```
## configurar contraseña para la consola
```
#config t
#line con 0 = puerto de consola
#password class
#login
#ex = exit
...
#service password-encryption
#w = write = graba toda la config del sistema
```
## poner una conexion ip al switch
```
#conf t
#interface vlan 1
#ip address 10.10.10.100 255.255.255.0
#no sh = no shutdown = levanta la ip
```
para saber que funciona en un pc se le asigna la ip y mask, y luego en la consola se hace ping

#
## Ejemplo

SW01: 200.34.128.254/24  
SW02: 200.34.128.253/24

- A 200.34.128.1/24 
- B 200.34.128.2/24
- C 200.34.128.3/24
- D 200.34.128.4/24
- E 200.34.128.5/24
- F 200.34.128.6/24
- G 200.34.128.7/24

1. poner nombre al switch
2. cifrar acceso a modo privilegiado con Cisco
3. cifrar acceso  consola con Class
4. encriptar contraseñas