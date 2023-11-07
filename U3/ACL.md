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



