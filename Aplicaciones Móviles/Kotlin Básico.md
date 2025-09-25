- ---
- #LenguajeDeProgramación
-  ---
## Creación de variables
Existen dos maneras para rear una variable, pueden ser las siguientes:
- **Var:** Creación de una variable que puede cambiar su valor en el resto del código.
- **Val:** Creación de una variable que su valor no va a cambiar nunca, es una variable constante.

``` kotlin
 // Ejemplos de creación de variables
 var soyUnaVariable
 val soyUnaVariableConstante
```

Al igual que en todos los lenguajes, hay tipos de variables, ya sean enteros, boleanos...
Para asignar a una variable que sea de un tipo u otro, después del nombre deberemos poner dos puntos y el tipo de variable.
Ojo cuidado que en kotlin las variables se ponen con la primera letra en mayúsculas, son consideradas directamente como Objetos.

``` Kotlin
var entero: Int
var decimal1: Float
var decimal2: Double
var boleano: Boolean
var cadena: String
var letra: Char
```

A las variables **var** podemos asignarle un valor predeterminado al crearlas, pero hay que tener cuidado ya que debemos tener en cuenta el valor nulo si es que no se le da.
El símbolo ? justo antes del signo = significa que puede tener tanto el valor null como cualquier valor según el tipo de variable que sea.

``` kotlin
var variable: Int? = 4
```

## Mostrar cosas en la consola
Para mostrar cosas por consola es muy parecido con python:
``` kotlin
var num1: Int? = 20

// Sin salto de línea
print("Hola tengo " + num1 + " años")

// Con salto de línea
println("Hola tengo " + num1 + " años")

// Agregando una variable dentro de las comillas
println("Hola tengo $num1 años")
```

## Condicional if y when
### Condicional if y uso del let
El condicional `if` nos sirve para redirigir el flujo de nuestro código dependiendo de una condición que pongamos.

``` kotlin
var numero: Int? = 5

if (numero == null) {
	println("Soy un numero nulo")
} else if (numero >= 0) {
	println("Soy un numero positivo")
} else {
	println("Soy un numero negativo")
}
```
En este ejemplo comprobamos si `numero` es **nulo** y, si no lo es, evaluamos si es positivo o negativo.

Aunque parezca que esto es todo, también podemos escribirlo de otra manera utilizando `let`.  `let` no reemplaza a `if`, pero combinado con el **safe call** `?.` nos permite ejecutar un bloque de código **solo si la variable no es nula**.

``` kotlin
var numero: Int? = 5

numero?.let {
    if (it >= 0) {
        println("Soy un número positivo")
    } else {
        println("Soy un número negativo")
    }
} ?: println("Soy un número nulo")

```
**Explicación:** 
- El operador **safe call** **`?.`** asegura que el bloque `let` se ejecute solo si `numero` **no es nulo**.
- Dentro del bloque de `let`, la variable se pasa automáticamente como **`it`**, por lo que **no es necesario usar el nombre original** (`numero`).
- El operador **Elvis (`?:`)** se ejecuta si `numero` **es nulo**, permitiendo definir un comportamiento alternativo.

💡 En otras palabras, `let` te permite **trabajar con el valor de la variable de manera segura y concisa**, evitando comprobaciones explícitas de null.

**Otras funciones de alcance (_scope functions_)**

| Función | Referencia al objeto | Modifica objeto? | Devuelve             | Función / Uso principal                                                               |
| ------- | -------------------- | ---------------- | -------------------- | ------------------------------------------------------------------------------------- |
| `apply` | `this`               | Sí               | El objeto            | Inicializar o configurar propiedades del objeto.                                      |
| `also`  | `it`                 | No               | El objeto            | Ejecutar acciones adicionales (logging, validaciones) sin modificar el objeto.        |
| `run`   | `this`               | Puede            | Resultado del bloque | Ejecutar un bloque de código y devolver un valor, usando el objeto dentro del bloque. |
Todas estas funciones pueden ser **encadenadas** después de los corchetes, permitiendo escribir código más limpio y seguro.

### Condicional when
En Kotlin, `when` es un condicional más **versátil y expresivo** que el clásico `if-else if-else` o `switch`.
Se usa para **evaluar un valor y ejecutar un bloque de código según diferentes casos**.

``` kotlin
val numero: Int? = 5

when (numero) {
    null -> println("Soy un número nulo")
    0 -> println("Soy cero")
    1 -> println("Soy uno")
    else -> println("Soy un número distinto de cero y uno")
}
```
**Explicación:**
- `when` compara el valor de `numero` con cada **caso** definido.
- Cada caso termina en `->` seguido del código que queremos ejecutar.
- `else` funciona como el `else` de un `if`, y se ejecuta si ningún caso coincide.
- Es **obligatorio** si no cubrimos todos los posibles valores (como con valores nulos o números no previstos).


`when` también puede **devolver un valor**, lo que evita usar variables temporales:

``` kotlin
val mensaje = when (numero) {
    null -> "Número nulo"
    0 -> "Cero"
    1 -> "Uno"
    else -> "Otro número"
}

println(mensaje)
```

Esto hace el código más conciso y legible.

**Comparaciones posibles (simples):**

|Caso|Ejemplo|
|---|---|
|Igualdad simple|`0 -> println("Cero")`|
|Varios valores juntos|`1, 2 -> println("Pequeño")`|
|Condición por defecto|`else -> println("Otro")`|
|Comprobar tipo|`is String -> println("Es texto")`|
## Operadores y constructos de rangos y colecciones
|Operador / Constructo|Uso principal|
|---|---|
|`in` / `!in`|Comprobar pertenencia en rango o colección|
|`..`|Crear rangos inclusivos|
|`until`|Crear rangos excluyendo el último valor|
|`downTo`|Rangos decrecientes|
|`step`|Definir salto en rangos|
|`indices`|Iterar sobre índices de listas/arrays|
|`lastIndex`|Obtener el último índice de una colección|
En Kotlin, existen varios **operadores y constructos** que permiten **comprobar pertenencia, definir rangos de valores y trabajar con colecciones de manera segura**.

``` Kotlin
val numero = 7
    if (numero in 1..5) println("Número entre 1 y 5")
    if (numero !in 1..5) println("Número fuera del rango 1 a 5")

    // 2️⃣ Uso de .. (rango inclusivo) en for
    println("\nRango inclusivo con ..")
    for (i in 1..5) print("$i ") // 1 2 3 4 5
    println()

    // 3️⃣ Uso de until (excluye último)
    println("\nRango con until")
    for (i in 0 until 5) print("$i ") // 0 1 2 3 4
    println()

    // 4️⃣ Uso de downTo (decremento)
    println("\nRango decreciente con downTo")
    for (i in 5 downTo 1) print("$i ") // 5 4 3 2 1
    println()

    // 5️⃣ Uso de step (salto)
    println("\nRango con step")
    for (i in 1..10 step 2) print("$i ") // 1 3 5 7 9
    println()

    // 6️⃣ Iterar sobre colecciones usando in
    val frutas = listOf("Manzana", "Banana", "Cereza")
    println("\nRecorriendo lista con in")
    for (fruta in frutas) println(fruta)

    // 7️⃣ Iterar usando indices
    println("\nRecorriendo lista usando indices")
    for (i in frutas.indices) {
        println("Elemento $i: ${frutas[i]}")
    }

    // 8️⃣ Usando lastIndex
    println("\nRecorriendo lista usando lastIndex")
    for (i in 0..frutas.lastIndex) {
        println("Elemento $i: ${frutas[i]}")
    }

    // 9️⃣ Uso de in en when
    val letra = "e"
    val vocales = listOf("a", "e", "i", "o", "u")

    when (letra) {
        in vocales -> println("\nEs una vocal")
        !in vocales -> println("\nNo es una vocal")
    }
```