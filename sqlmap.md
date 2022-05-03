# Usando sqlmap

- `-D` nombre de una db
- `-T` nombre de una tabla
- `--dump` mostras todos los datos en la db si solo se uso -D, o todos los datos en la tabla si se usa -D -T.

- uso basico:
    - `sqlmap -u http://sitio.com/login?id=1 --dbs` buscar bases de datos.
    