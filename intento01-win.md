# intento de ataque a maquina windows 01.
### intento-win-01
##### 30-dic-2022

1. Escanear ip activos en la red.
    - `nmap -sn 192.168.100.1/24`
        - `-sn` Ping Scan - disable port scan
        - `192.168.100.1/24` [marcara de red](/marcara-de-redm.md) 255.255.255.0 
2. Escanear puertos
    - `nmap -Sv -sC -O -n -oX scan.xml 192.168.100.1/24
        - `-Sv` Probe open ports to determine service/version info
        - `-sC` equivalent to --script=default
        - `-O` Enable OS detection
        - `-n` /-R Never do DNS resolution/Always resolve [default: sometimes]
        - `-oX scan.xml` salida xml a scan.xml, se puede editar el xml y cambiarle el stylesheet por uno mas descriptivo como
        [nmap-bootstrap-xsl](https://github.com/honze-net/nmap-bootstrap-xsl)

        - `--stylesheet https://raw.githubusercontent.com/honze-net/nmap-bootstrap-xsl/master/nmap-bootstrap.xsl` para agregar el
        **nmap-bootstrap-xsl** de forma automatica. 

        - `192.168.100.1/24` [marcara de red](/marcara-de-redm.md) 255.255.255.0 

3. puertos abiertos
    - `135` Microsoft Windows RPC
    - `139` Microsoft Windows netbios-ssn
    - `445` microsoft-ds
    - `5357` Microsoft HTTPAPI httpd

4. volvemos a escaner ahora con `-p-` para escanear todos los puertos.
    - `49668` Microsoft Windows RPC

5. volvermos a escanear todos los puertos pero ahora con UDP. `-sU` quedaria asi `sudo nmap -sV -sC -O -n -oX scan3.xml --stylesheet https://raw.githubusercontent.com/honze-net/nmap-bootstrap-xsl/master/nmap-bootstrap.xsl 192.168.100.120 -p- -sU`

6. buscamos vulns en el puerto http `5357` con `nikto -h 192.168.100.120:5357` 


<br>

> In windows all the passwords are stored in NTLM Form and are stored in SAM file.