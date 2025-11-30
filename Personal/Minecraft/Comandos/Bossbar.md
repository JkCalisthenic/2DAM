- --
- Tags: #Personal #Minecraft #Comandos
- --
Con el comando bossbar se podrán crear barras de bosses a cualquier mob

Con `/bossbar add < id > < name >`  creará una barra de boss.
- `id` -> Se usa para apuntar a la barra principal y tiene la forma `namespace:name`, por ejemplo: `foo:bar`. Si no se especifica `namespace`, el valor predeterminado es `minecraft`.
- `name` -> Es el nombre para mostrar de la barra principal y solo acepta un componente de texto JSON


`/bossbar set <id> nombre <name>` cambiará el nombre de la barra de jefe.
`/bossbar set <id> color <color>` cambiará el color del texto (si no se especificó ningún color como parte de un componente de texto) y la barra de jefe, por defecto es `blanco</ código>.`
`/bossbar set <id> style <style>` cambiará el estilo de la barra de jefe, el valor predeterminado es `progreso`.
- Las opciones disponibles son: `notched_6`, `notched_10`, `notched_12`, `notched_20` y `progress`.
- `notched` establecerá la cantidad de segmentos.
- `progress` establecerá la cantidad de segmentos en 1.

`/bossbar set <id> valor <value>` cambiará el valor actual de la barra de jefe, el valor predeterminado es `0`.`
`/bossbar set <id> max <max>` cambiará el valor máximo de la barra de jefe, el valor predeterminado es `100`.
 `/bossbar set <id> visible <visible>` cambiará la visibilidad de la barra de jefe, por defecto es `true` 
 `/bossbar set <id> players <players>` cambiará qué jugadores pueden ver la barra de jefe, el valor predeterminado es ninguno.
 `/bossbar remove <id>` eliminará la barra de jefe.
 `/bossbar list` mostrará una lista de barras de jefe creadas.
 `/bossbar get <id> (max|jugadores|valor|visible)` devolverá la configuración solicitada como un `result` del comando
 