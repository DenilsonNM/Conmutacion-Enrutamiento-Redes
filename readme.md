# Apuntes

## datos y puntos importantes
- la ip config DNS asiga nombres a una direccion IP
- Router SOHO = Small office/ Home office

- una trama ethernet tiene 1518 octeto (8 bits), en la capa 2 y la otra trama es la iee 802.3 tambien con 1518
- fastethernet le toma 9 microsegundos enviar 1518
- velocidad de quire spick 14400 tramas en un segundo, velocidad de aprendisaje de un switch

### IPv4:
- la malloria de las compus son UniCast (solo una pagina a la vez)
- broadCast (envia a todas las redes, se usa para saber que equipos hay en una red)
- Clase A: redes grandes 0.0.0 - 127.255.255 looppack (Lo que llama localHost, se llama asi misma), no se usan (1 octeto para red y 3 para host, 
 puede tener 14 millones de host)
- clase B medianas: 128.0.0.0 - 191.255.255 se usa pocas veces, 2 octetos para red y 2 para host (65,535 host)
- clase C: 192.0.0.0 - 223.255.255, 3 octetos para 3 y 1 para host (254 host)
- clase D multicast (envia multiples nodos espesificos, no a todos, como netflix)

# 
## Capas del modelo OSI
### 1 fisica
verificar que este conectado los cables

### 2 enlace
verificar si exise enlace entre equipos

### 3 red
verificar la direccion de red que deben tener los equipos, direccionamiento logico, establece la ruta para llegar a tu destino

### 4 aplicacion
ofrece a las aplicaciones la posibilidad de acceder a los servicios de las demas capas
# 
## reglas del funcionamuento de los rangos de red
1. cuando todos los bits en host id esten en 0, esto significa la direccion de la red
ejemplo: 200.34.128.0

2. cuando todos los bist en hot id esten en 1, es el broadCast de esa red
ejemplo 200.34.128.255

3. el rango que hay entre la direccion de red y broadcast corresponde al ambito de la red, lo que puede ver en la red
ejemplo 200.34.128.1 hasta 200.34.128.254 

4. NetMask (mascara de red): debo de ponerle 1 a todo lo que corresponda la red y 0 a todo lo que corresponda el host
    - clase A: 11111111 00000000 00000000 00000000 = 255.0.0.0
    - Clase B: 11111111 11111111 00000000 00000000 = 255.255.0.0 (pero tambien se puede cambiar por el usuario)

#
## Ejemplo: 10.14.32.1/24
- mascara de red: 255.255.254.0
- 11111111 11111111 11111110 00000000
- dir de red: 10.14.32.0
- dir broadcast: 10.14.33.255
- ambito: 10.14.32.1 hasta 10.14.33.254 (para representar los bits prendidos se usa la diagonal)

### EJEMPLO 1
- 10.10.10.10.1/30
- DR: 10.10.10.0
- BC: 10.10.10.3
- 4x8 = 32
    - 11111111 11111111 11111111 11111100 = 30 prendidos y 2 apagados
- la mascara 00000001 en 1 binario, aplicando la regla 2, se prenden los 2 ultimos digitos del 1 en binario, y queda: 00000011 = 3

### EJEMPLO 2
- 10.14.16.40/22
- DR: 10.14.16.0
- BC: 10.14.19.255
- 11111111 11111111 11111100 00000000 = 22 prendidos y en el 3ro esta el corte, osea que el octeto que tiene el 16 sera el que se usa para BC
- 16 en binario es 00010000, para el BC se prenden los 2 ultimos digitos de 16 en binario y queda 00010011 = 19
---
# Apuntes 2
## Normas de cableado
- T568B: todos siguen esa
- T56SA es cuando se usa un cable cruzado
- 568 espesifica y dice el diseño del cableado, redes de datos, telefono y video
- 569 son rutas, distancia a enlazar, donde se pueden poner los raks, distancias de paredes, ventanas, iluminacion del area
- 606 mapas de direcciones ips, nodos con nomenclatura, como rematan los nodos para identificar
- 607 tierras fisicas, como evitar que el equipo se dañe, para que sirven los equipos

### ubicacion de cable en un rack:
- nodos de izq a der (equipos)
- enlaces de der a izq (routers)

### direccionamiento IP:
- de abajo hacia arriba para pc
- arriba hacia abajo los enlaces

#
### Datos
- switch aprenden por direcciones MAC
- MAC esta formada de 6 octetos, es la direccion fisica, cada equipo tiene diferente
- primera mitad es OI (identificador del fabricante el que hace la targeta de red)
- la otra el numero de control que tiene el fabricante
14 millones de opciones diferentes por lado
01 AB T5 31 - 4H HY NA DD

- capa1 = hub/concentrador = replica la direccion y se lo mande a todos (-->) (inundacion se usa para saber quien mando la direccion y se manda a todos)
- capa2 = puende/switch, conmutador de datos (--><--)
- capa3 = direccionamiento de red, switch enrutan el paquete a su destino independiente del camino
- default gateway es el punto de partida donde se puede tomar la ruta a su destino, para poder conectar 2 redes