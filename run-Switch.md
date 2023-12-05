Configuración básica de un Swich Cisco By LMota

1. Definición del Hostname
hostname <Nombre del Host>

2. Definición de las VLAN
interface vlan <Vlan-Tag>
description <Descripcion de la VLAN>
ip address <Dirección IP> <Mascara> 

3. Asignar Puertos a la VLAN
interface [range] fastethernet 0/<puerto-inicial>-[puerto-final]
swtchport mode <Trunk/access>
shitchport <access/Trunk> Vlan <Vlan-Tag> 

4. Habilitamos el Forwarding (Teniendo multiples VLANS)
ip routing

5. Definimos el Gateway por defecto
ip default <IP router> 

6. Habilitando el servicio SSH
ip ssh server
crypto key generate rsa 

6. NO OLVIDAR PARA SWITCHES DE CAPA 3!!!
Si el puerto es trunk agregar :
switchport trunk encapsulation dot1q   <--- antes de Switchport mode trunk

Cada ruta interna deberá ser agregada en el router CISCO
