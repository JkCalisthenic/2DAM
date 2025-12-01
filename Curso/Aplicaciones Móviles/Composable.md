- ---
- Tags: #AplicacionesMoviles #LenguajeDeProgramación #Kotlin #Clase
- --
# Qué es un composable
En **Kotlin**, un **Composable** es una **función especial** utilizada en **Jetpack Compose**, el framework moderno de Android para construir interfaces de usuario declarativas.

**En resumen:**  
Un `@Composable` es una función que **describe cómo debe verse una parte de la interfaz de usuario** (UI), en lugar de decirle al sistema _cómo dibujarla paso a paso_.

## Qué hace realmente un `@Composable`

Cuando marcas una función con `@Composable`, le dices al compilador que esa función **puede generar UI** y que **puede ser llamada desde otras funciones composables**.  
Por ejemplo:

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hola, $name!")
}
```

## Parámetros de un `@Composable`
Casi todos los Composables en Jetpack Compose pueden recibir parámetros que controlan **su apariencia, posición y comportamiento**.  
Los más comunes son:

### `Modifier`
Es un **objeto** que sirve para **modificar la apariencia o el comportamiento** de un Composable.  
Se usa para aplicar cosas como:

- Tamaño (`.size()`, `.width()`, `.height()`)
- Color o fondo (`.background()`)
- Margen o espacio (`.padding()`)
- Alineación (`.align()`)
- Reacciones a clics (`.clickable()`)

```kotlin
Text(
    text = "Hola Compose!",
    modifier = Modifier
        .background(Color.Yellow)
        .padding(16.dp)
)
```

## Tipos de `@Composable` Básicos
### **Box**

Sirve para **superponer** elementos (uno encima del otro) o **alinear un único elemento** dentro de un espacio.
```kotlin
@Composable
fun BoxEjemplo() {
    Box(
        modifier = Modifier
            .size(120.dp)
            .background(Color.Gray),
        contentAlignment = Alignment.Center // Centra el contenido dentro
    ) {
        Text("Dentro del Box")
    }
}
```

### **Column**

Organiza elementos **uno debajo del otro (verticalmente)**.
```kotlin
@Composable
fun ColumnEjemplo() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally // Alineación horizontal de los hijos
    ) {
        Text("Primer elemento")
        Text("Segundo elemento")
        Button(onClick = {}) {
            Text("Botón")
        }
    }
}
```

### **Row**

Organiza elementos **uno al lado del otro (horizontalmente)**.
```kotlin
@Composable
fun RowEjemplo() {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .background(Color.LightGray),
        horizontalArrangement = Arrangement.SpaceEvenly // Espaciado entre hijos
    ) {
        Text("Inicio")
        Text("Centro")
        Text("Final")
    }
}
```

### **Text**

Muestra texto en pantalla.
```kotlin
@Composable
fun TextEjemplo() {
    Text(
        text = "Hola Mundo",
        fontSize = 20.sp,
        color = Color.Blue,
        fontWeight = FontWeight.Bold
    )
}

```

### **Image**

Muestra una imagen desde recursos o desde un objeto `Painter`.
```kotlin
@Composable
fun ImageEjemplo() {
    Image(
        painter = painterResource(id = R.drawable.logo), // imagen en res/drawable
        contentDescription = "Logo de la app",
        modifier = Modifier.size(100.dp),
        contentScale = ContentScale.Crop // cómo se ajusta la imagen al espacio
    )
}
```

