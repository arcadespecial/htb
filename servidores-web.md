# Buscar vulnerabilities en Servidores Web.

- Nikto
    - `nikto -h example.com`

- Web Fuzzer (*remplazo de palabras en el url*)
    - `wfuzz -c -z range,1-10 http://www.sitio.com/FUZZ` la palabra **FUZZ** seria remplazada por numeros del 1 al 10.
    - `wfuzz -c -z file,palabras.txt http://www.sitio.com/FUZZ` palabra **FUZZ** seria remplazada por las palabras dentro del archivo.
    - con la opcion `--sc` fitramoslos resultados, p.e. `--sc 200` solo muestra los resultados con *200 OK.f* 
    - `-c` muestra la salida con colores
    - `-w palabras.txt` lo mismo q usar file,palabras.txt
    - `-L` seguir redirecciones.
    - `-H` header p.e. `-H "Host: FUZZ.sitio.htb"

- Checar **JWT** en las cookies.
    - normalmente inician con `eyJ0eXAiOi`   
    - jwt que contengan `jku` por ejemplo `"jku": "http://hackmedia.htb/static/jwks.json"` 
        - https://blog.pentesteracademy.com/hacking-jwt-tokens-jku-claim-misuse-2e732109ac1c 

- Crear un servidor con python3 en el directorio actual
    - `python3 -m http.server 9000`
