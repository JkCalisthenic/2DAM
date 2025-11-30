- --
- Tags: #Personal #Minecraft #Comandos
- --
`/return` se usa dentro de una función (es decir, en un archivo `.mcfunction`).

Sirve para detener la ejecución de esa función en el punto donde se coloca y/o devolver un valor entero arbitrario como “valor de retorno”.

Esto permite, por ejemplo, que —si la función tiene ramas condicionales— puedas usar `/return` para indicar cuál rama se tomó, y luego ese valor se pueda usar en otra función o comando.

# Sintaxis
`/return <valor>` -> Termina la función y devuelve el entero de `<valor>` como resultado.
`/return run <command>` -> Ejecuta `<command>`, luego termina la función y usa el "valor de retorno" del comando ejecutado como valor de retorno de la función. Si el comando falla devuelve 0.

- < valor > debe ser un entero válido de 32 bits.
- < command > puede ser cualquier comando válido.

# Resultado
- Cuando se usa `/return <valor>`: la función finaliza con éxito, y su "valor de retorno" será `<valor>`.
-  Si se usa `/return run <command>`: la función se detiene tras ejecutar `<command>`; si `<command>` tuvo éxito, la función retorna el "resultado" de ese comando; si falló, la función retorna 0.
- Si la función no ejecuta ningún `/return`, entonces es "void": no retorna valor ni éxito/fallo.

Además, si la función fue invocada mediante `/function`, el valor de retorno y el estado de éxito se devuelven a ese comando `/function`, lo que permite usar ese resultado en otras funciones/comandos.
