# NAT estatica
148.208.144.1-5
192.108.0.0

ip nat pool NAT-POOL 148.208.144.1 148.208.144.5
access-list 1 permit 192.108.0.0 0.0.255.255
ip nat inside source-list 1 pool NAT-POOL
exit
int gi0/0
ip nat inside 
int gi0/1


# PAT
agarrar una direccion de red y asignarle un numero dinamico de puerto
una ip para varias
ip nat inside source-list 1 pool NAT-POOL overlord