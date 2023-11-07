# Apuntes IPV6
para ipv6 lo primero se configura el router pq se pueden asignar direcciones fijas o dinamicas EUI64
```
en
config t
...
ipv6 unicast-routing
int gi 0/0/0
ipv6 add add 2020:db8:acad:1::100/64
ipv6 add fe80::1 link-local
no shut
```
```
int gi 0/0/1
ipv6 add 2020:db8:acad:2::100/64
ipv6 add fe80::2 link-local
```

---

### Routeo estatico "ip route network-address subnet-mask"
- une 2 redes entre unicos caminos de routers ruta preterminada: 0.0.0.0.0

### rutas de respaldo ""
- mandar a preguntar a otro router que router es el destino

### rutas alternativas
- ipv6 route ::/0 2000:ACAD:F0C0:1::2
- ipv6 route 2001:DB8:1:2::/64 2001:DB8:1:A001::2