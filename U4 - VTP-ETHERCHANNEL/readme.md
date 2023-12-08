# VTP

(VLAN Trunking Protocol) conjunto de switches trunked que tienen configuraciones VTP coincidentes (nombre del dominio, contraseña y versión de VTP

```
show vtp status
```

### Servidor VTP

```
vtp mode server
vtp domain ejemplo.com
vtp password Cisco
```

### Cliente VTP

```
vtp mode client
vtp domain ejemplo.com
vtp password Cisco
int range fa0/20-24
sw mo trunk
```

---
# EtherChannel

Permite agrupar varios enlaces Ethernet físicos en un solo enlace lógico

```
sw int port-channel <numero>
```

### STP (Spanning Tree Protocol)
Protocolo de red que previene los bucles de red en topologías con enlaces redundantes, de manera predeterminada STP los bloquea

## PAgP

- `on` miembro del canal sin negociación (sin protocolo)
- `desirable` pregunta activamente si el otro lado puede participar o si va a hacerlo
- `auto` espera pasivamente al otro lado

```
int range fa0/1-2
channel-g 1 mode desirable
channel-protocol pagp ***
int port-channel 1
sw mo trunk
sw tr allowed vlan 1,2,20
```

## LACP

- `on` miembro del canal sin negociación (sin protocolo)
- `active` pregunta activamente si el otro lado puede participar o va a hacerlo
- `passive` espera pasivamente al otro lado

```
int range fa0/1-2
channel-g 1 mode active
channel-protocol lacp ***
int port-channel 1
sw mo trunk
sw tr allowed vlan 1,2,20
```
