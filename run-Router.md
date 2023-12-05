Configuración básica de un Router By LMota

1. Definición del Hostname
hostname <Nombre del Host>

2. Dewfinición del DNS
ip name-server <IP DNS>

3. Definición de las Interfaces
interface <Tipo de Interfaz>
description <Descripción de la Interfaz>
ip address <Dirección IP> <Mascara> [secondary]
**** NOTA ****  Si la interfaz usa DHCP deberá escribir ip address dhcp
ip access-group <Lista de Acceso> <in / out>
ip nat inside/outside   <---- Optativo. Si raliza NAT
duplex auto
speed auto
keepalive 20 <--- Optativo 
no shutdown   <----- Nunca olvidemos levantar la interfaz

4. Definición del Ruteo estático
ip route 0.0.0.0 0.0.0.0 <Ip-frontera.out>      <--- Origen Cualquiera, destino cualquiera, a quien pregunta
ip route <origen> <mask> <gateway-borde>

5. En caso de ejecutar RIP y no ruteo estático
router rip
versión 2
network <Red-01 que tiene el Router>
network <Red-02 que tiene el Router>
(Repetir por cada una de las redes)
NOTA ... RIP trabaja con otros equipos que hablen RIP

6. En caso de ejecutar el Protocolo de frontera (BGP)
router bgp <Sistema Autóno>
no synchronization
bgp log-neighbor-changes
network <Red a aprender> mask <Mascara>
no auto-summary

7. Algunas acciones de seguridad, para evitar entren por web (en algunos casos)
no ip http server
no ip http secure-server

8. Defiición de las direcciones a ser NATEADAS
ip nat pool <NombrePool> <Ip-Publica-INicio> <Ip-Publica-fin> netmask <Máscara>
ip nat inside source list <Nombre-Lista de IPs a Natear> pool <Nombre del Pool> overload

9. Definición de quienes serán Nateados
ip access-list extended <Nombre-Lista de IPs a Natear>
permit ip IPs-Internas-A-Natear> <Mascara-Invertida> any

10. Listas de acceso
ip access-list extended <Nombre-Lista-Acceso>
deny ip host <ip-host> any
deny ip <red-interna> <mask invertida> host <ip destino>
deny ip <red-externa> <Mask-Invertida> any
deny <tcp/udp> any any eq <puerto>
---AL FINAL
permit ip any any


Optativo!!
Configuración DHCP
1. Asignar IP a la INterfaz (del mismo rango)

2. asignar las exclusiones
   ip dhcp excluded-address <ip>
   ip dhcp excluded-address <ip-inicial> <ip-final>

3. asignar el pool DHCP
   ip dhcp pool MI-DHCP       <----- No olviden mayusculas
      network <red> <Mascara> <----- de la misma red que la interfaz
      default-router <IP>     <----- dirección del enrutador
      dns-server <ip>         <----- Servidor de Nombres

Listo!!
