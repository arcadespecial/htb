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
    - normalmente inician con `eyJ0eXAiOi` o com `ey` que es el `{` de json   
    - jwt que contengan `jku` por ejemplo `"jku": "http://hackmedia.htb/static/jwks.json"` 
        - https://blog.pentesteracademy.com/hacking-jwt-tokens-jku-claim-misuse-2e732109ac1c -- si `getPublicParams.py` da error *No module named 'Crypto'* usar `pip install Crypto` si falla usa `pip install pycryptodome==3.14.1`
        - si esta limitado al directorio del servidor, osea solo a `http://hackmedia.htb/static/` se usa: `"jku": "http://hackmedia.htb/static/../redirect?url=10.10.14.83:8888/jwks.json"`
        - al parecer el metodo esta **incorrecto**, usar https://mkjwk.org/ con parametros: `2048,Signature,RS256,SHA-256,Yes` para generar los archivos, ya no es necesario el uso de `getPublicParams.py`, usar los valores de `"n"` que entrega la pagina para actualizar el archivo jwks.json y el public key y private key para generar el token en la pagina `https://jwt.io/`
        
        - [metodo q si funciona, esta en chino](https://zhuanlan.zhihu.com/p/446176672) 

        - usar extension de chrome `Cookie-Editor` para modificar la cookie una vez q funciono en el repeater del burp.

- Crear un servidor con python3 en el directorio actual
    - `python3 -m http.server 9000`
    - `python3 -m http.server --bind 10.10.14l83 9000`, asi se hace bind solo en una ip.
