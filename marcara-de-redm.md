# Marcara de red.


#### Metodología
Mediante la máscara de red, un sistema (ordenador, puerta de enlace, enrutador, etc.) podrá saber si debe enviar un paquete dentro o fuera de la subred en la que está conectado. Por ejemplo, si el enrutador tiene la dirección IP 192.168.1.1 y máscara de red 255.255.255.0, entiende que todo lo que se envía a una dirección IP con formato 192.168.1.X, se envía hacia la red local, mientras que direcciones con distinto formato de dirección IP serán enviadas hacia afuera (Internet, otra red local mayor, entre otros). 


#### si escribimos `192.168.100.1/24` significa que la marcar es `255.255.255.0` por que `\24` significa 24 bits desde el lado izquiero es decir `11111111.11111111.11111111.00000000`.
