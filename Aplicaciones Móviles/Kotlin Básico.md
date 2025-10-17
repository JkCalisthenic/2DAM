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

En Kotlin, existen varios **operadores y constructos** que permiten **comprobar pertenencia, definir rangos de valores y trabajar con colecciones de manera segura**.

``` Kotlin
// 1️⃣ in y !in con if
val numero = 7
if (numero in 1..5) println("Número entre 1 y 5")
if (numero !in 1..5) println("Número fuera del rango 1 a 5")

// 2️⃣ .. (rango inclusivo)
if (3 in 1..5) println("3 está en el rango de 1 a 5")

// 3️⃣ until (excluye último)
if (5 !in 0 until 5) println("5 no está en el rango 0 until 5") // 0..4

// 4️⃣ downTo (decremento)
if (3 in 5 downTo 1) println("3 está en el rango 5 downTo 1")

// 5️⃣ step (salto)
if (4 in 0..10 step 2) println("4 está en el rango 0..10 con step 2") 
// 0,2,4,6,8,10

// 6️⃣ in con colecciones
val vocales = listOf("a", "e", "i", "o", "u")
val letra = "e"

if (letra in vocales) println("$letra es una vocal")
if ("x" !in vocales) println("x no es una vocal")

// 7️⃣ Uso de when con in y !in
when (numero) {
	in 1..5 -> println("Número entre 1 y 5")
    in 6..10 -> println("Número entre 6 y 10")
    !in 1..10 -> println("Número fuera de 1 a 10")
}
```

| Operador / Constructo | Uso principal                              |
| --------------------- | ------------------------------------------ |
| `in` / `!in`          | Comprobar pertenencia en rango o colección |
| `..`                  | Crear rangos inclusivos                    |
| `until`               | Crear rangos excluyendo el último valor    |
| `downTo`              | Rangos decrecientes                        |
| `step`                | Definir salto en rangos                    |
| `indices`             | Iterar sobre índices de listas/arrays      |
| `lastIndex`           | Obtener el último índice de una colección  |
## Listas
### List (inmutable)
- Es **solo de lectura**: no puedes agregar, eliminar ni cambiar elementos después de crearla.
- Ideal para listas que no deben cambiar.

```kotlin
val numeros = listOf(1, 2, 3, 4)
println(numeros[0]) // 1
// numeros.add(5) ❌ Error: no se puede modificar
```

### MutableList
- Es **mutable**, puedes agregar, eliminar y modificar elementos libremente.

```kotlin
val numeros = mutableListOf(1, 2, 3)
numeros.add(4)      // ✅ Agregar
numeros.remove(2)   // ✅ Eliminar
numeros[0] = 10     // ✅ Modificar
println(numeros)    // [10, 3, 4]

```

### ArrayList
- Crea una **lista basada en ArrayList de Java**.  
Es prácticamente igual que mutableListOf, pero garantiza la implementación concreta.

```kotlin
val lista = arrayListOf("a", "b", "c")
lista.add("d")
println(lista) // [a, b, c, d]

```

### EmptyList y EmptyMutableList
- Crean listas vacías sin elementos.

```kotlin
val listaVacia = emptyList<String>()
val listaMutableVacia = mutableListOf<Int>()

```

### ListOfNotNull 
- Crea una lista que **omite los valores nulos** automáticamente.

```kotlin
val lista = listOfNotNull(1, null, 3, null, 5)
println(lista) // [1, 3, 5]

```

## Clases
Una clase en kotlin se define con sus atributos:
```kotlin
// Definición de la clase Persona
class Persona(
    var nombre: String,    // Atributo 1
    var edad: Int,         // Atributo 2
    var ciudad: String     // Atributo 3
) {
    // Función para mostrar información de la persona
    fun mostrarInfo() {
        println("Nombre: $nombre, Edad: $edad, Ciudad: $ciudad")
    }
}
```

En este caso hemos creado la clase Persona, la cual tiene nombre, edad y ciudad.
Si quisiéramos utilizar y acceder a la información de la clase:
```kotlin
fun main() {
    val persona1 = Persona("Ana", 25, "Madrid")
    persona1.mostrarInfo()
}
```
Primero crearíamos una variable donde guardamos a la Persona pasándole los parámetros desus atributos.
Y después podemos acceder a sus métodos mucho más fácil que en java:

```kotlin
fun main() {
    val persona1 = Persona("Ana", 25, "Madrid")
    persona1.mostrarInfo()
    
    println(persona1.nombre)
    println(persona1.edad)
    println(persona1.ciudad)
}
```


### Herencia
La herencia permite que una clase herede propiedades y métodos de otra clase, evitando repetir código.
#### Clase base o padre
Para permitir que otra clase herede de ella, la clase debe marcarse con la palabra clave open.
Por defecto, las clases en Kotlin son final (no se pueden heredar).

```kotlin
open class Persona(
    val nombre: String,
    val edad: Int
) {
    fun saludar() {
        println("Hola, mi nombre es $nombre")
    }
}

```
#### Clase derivada o hija
Se crea usando `:` seguido del nombre de la clase padre.
Debes llamar al constructor del padre si tiene parámetros.

```kotlin
class Estudiante(
    nombre: String,
    edad: Int,
    val carrera: String
) : Persona(nombre, edad) {   // Hereda de Persona

    fun estudiar() {
        println("$nombre está estudiando $carrera")
    }
}

```

#### Sobrescribir métodos
Para permitir que un método sea sobrescrito, la función del padre debe ser open.
En la clase hija se usa `override` para modificarlo.

```kotlin
open class Persona(
    val nombre: String
) {
    open fun presentarse() {
        println("Hola, soy $nombre")
    }
}

class Profesor(nombre: String, val materia: String) : Persona(nombre) {
    override fun presentarse() {
        println("Hola, soy $nombre y enseño $materia")
    }
}

```

#### Uso de super
Dentro de la clase hija, super se usa para llamar a métodos de la clase padre.

```kotlin
class Profesor(nombre: String, val materia: String) : Persona(nombre) {
    override fun presentarse() {
        super.presentarse()  // Llama al método de Persona
        println("Mi materia es $materia")
    }
}

```

### Clase public
- En Kotlin, todas las clases son public por defecto.
- Esto significa que pueden ser accedidas desde cualquier parte del proyecto.
- No necesitas escribir public explícitamente, pero puedes hacerlo si quieres ser más claro.

```kotlin
public class Vehiculo(val marca: String, val modelo: String)

fun main() {
    val miCoche = Vehiculo("Toyota", "Corolla")
    println(miCoche.marca)  // Toyota
}

```

### Clases sealed
- Una clase sealed permite controlar todas las subclases posibles.
- Es útil cuando quieres que todas las variaciones de una clase estén en el mismo archivo.
- Muy usado en when para cubrir todos los casos sin necesidad de else.

```kotlin
sealed class Resultado
class Exito(val mensaje: String) : Resultado()
class Error(val codigo: Int) : Resultado()

fun mostrarResultado(res: Resultado) {
    when (res) {
        is Exito -> println("Éxito: ${res.mensaje}")
        is Error -> println("Error: ${res.codigo}")
    }
}

fun main() {
    val res1: Resultado = Exito("Todo salió bien")
    val res2: Resultado = Error(404)

    mostrarResultado(res1)  // Éxito: Todo salió bien
    mostrarResultado(res2)  // Error: 404
}

```

