# Direccionamiento ipv6

- Nace pq se alacanzo el limite de ipv4 - 4 mil millones de direcciones posibles y se acabaron

- 128 bits en formato hexadecimal (0-9) (A-F)
cada 4 digitos hex, son equivalentes a 16 bits
8 hextetos, 16 bits por octeto

- la red va de izq a der y de der a izq el host
tiene 64 bits por cada host 64 elevado a 264
transmision maxima (MTU) de mas de 1280 bytes
es mas seguro, pero menos privasidad
IPsec encryption

---
2001:0DB8:0001:5270:0127:00AB:CAFE:0E1F/64

- primeros 3 hecteros = global routing prefix 2 elevado a 48 = 4 mil millones de lugares, asignado por el proveedor de servicio
- el 4to hecteto = subnet ID = region, las diviciones internas de cada unos de los proveedores de servicio
- el resto = interface ID = nombre de host ID, el equipo en cuestion, se asigna EUI-64 (identificador unico de la interfaz) o manual,
- EUI usa los 48 bits de la Direccion MAC y añade FF:FE para que sea 64 bits
- No tiene bloadcast, usa direcciones multicast
---
usa el mismo metodo que ipv4 para subnet sus direcciones
- /127 da 2 direcciones
- /124 da 16
- /120 da 256
- primera direccion es 0, la ultima F
---

## Como compactar direcciones IPV6:
- 2001:0DB8:0001:5270:0127:00AB:CAFE:0E1F/64
    - 2001:DB8:1:5270:127:AB:CAFE:E1F/64

- 2001:0DB8:0000:0000:ACAD:0000:0000:E175/64
    - 2001:0DB8::ACAD:0:0:E175/64

## Link local ipv6
- direccion EUI: mack
---
## Tipos de IPV6

- double stack una ipv4 y ipv6 pueden estar juntas, pero las maquinas solo pueden ver paquetes de su tipo
- Unicast: activa la conexion ipv6
- Multicast: interfaz se identifica con su direccion reservada FF00::0/8
- Anycast: es un tipo de bloadcast, pero manda paquetes a sus dispositivos cercanos, les dice cual es sus protocolos de ruteo 

- Link-local: direccion adicional de un equipo que dice cual es el enlace local para llegar a otra, se usa FE80::X/10, 
- los routers no envian paquetes con esto, solo los recibe, no es enrutable a otras direcciones
- Loopback: similar a ipv4, se escribe ::1 para saber si estoy en una red
---
IANA = asigna globalmente le grupo de direcciones que va a tener cada uno
- APNIC
- ARIN
- RIPE

luego:
- ISP
- Site
- Subred

# opcion de SLAAC
### ipv6 managed-config-flag
- poner direcciones ipv6 espesificas de modo dinamico a las pc
### ipv6 nd other-config-flag
- pener DNS, dominio y datos adicionales

por defecto cisco trae estas 2 banderas apagadas