# Uso basico de nmap

- Solo listar un rango de ips:
    - `nmap -sL -n 192.168.100.1/24` el rango esta entre **192.168.100.0** a **192.168.100.255** se definie con **/24** que es la [mascara de red](/marcara-de-redm.md)
    - `nmap -sL -n 192.168.0.0/16` el rango esta entre **192.168.0.0** a **192.168.255.255**