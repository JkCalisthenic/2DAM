- ---
- Tags: #Personal #LenguajeDeProgramación #Java #Librería
- --
# GLFW para creación de ventanas
## .glfwInit():
1. Inicializa la librería GLFW completa
	Configura todos los subsistemas internos necesarios para que GLFW funcione (ventanas, manejo de input, creación de contextos gráficos, manejo de errores, etc.).

2. Prepara los recursos del sistema operativo
	Esto incluye cosas como:
	- Configuración de temporizadores y eventos.
	- Comunicación con el sistema de ventanas (X11, Wayland, Win32, Cocoa, etc.).
	- Carga de extensiones o dependencias necesarias.

3. Habilita el sistema de error de callbacks
	Después de llamar a glfwInit(), puedes configurar glfwSetErrorCallback() para capturar errores de GLFW.

4. Devuelve un booleano indicando éxito o fallo
``` java
if (!glfwInit()) {
    throw new IllegalStateException("No se pudo inicializar GLFW");
}
```
Si devuelve `false`, significa que el entorno no pudo inicializarse (falta de permisos, problemas de drivers, error en sistemas gráficos, etc.).

4. Debe llamarse solo una vez
5. Requiere una llamada a glfwTerminate() al final

## .glfwCreateWindow(width, height, title, NULL, NULL)
El método **`glfwCreateWindow(width, height, title, NULL, NULL)`** crea una **ventana** y un **contexto OpenGL** (o Vulkan, según configuración) usando GLFW a través de LWJGL.

Crea una ventana en el sistema operativo
Genera una ventana nativa con:
- Ancho: width
- Alto: height
- Título: title

Ejemplo:
``` java
long window = glfwCreateWindow(800, 600, "Mi Juego", NULL, NULL);
```
El significado del primer NULL es el parámetro que define el monitor donde se abrirá la ventana.

- Null-> ventana normal, en modo ventana (windowed).
- Si se pusiera un monitor válido, por ejemplo obtenido por glfwGetPrimaryMonitor(), sería fullscreen exclusivo
Ejemplo fullscreen:
``` java
glfwCreateWindow(1920, 1080, "Juego", glfwGetPrimaryMonitor(), NULL);
```

El último NULL indica si la ventana comparte recursos OpenGL con otra.
- NULL -> no comparte contexto con nadie
- Si se pone otro contexto válido pueden compartir texturas, buffers, shaders, etc.

Ejemplo:
```java
glfwCreateWindow(800, 600, "Ventana 2", NULL, window1);
```

Este método devuelve un long que representa el handle (identificador) de la ventana.
Si falla, devuelve NULL (0).
Por eso siempre se comprueba:
```java
long window = glfwCreateWindow(800, 600, "Mi Ventana", NULL, NULL);
if (window == NULL) {
    throw new RuntimeException("No se pudo crear la ventana");
}
```

## .glfwMakeContextCurrent(window)
Este método sirve para activar el contexto OpenGL asociado a la ventana que se creó con glfwCreateWindow

Básicamente es que a partir de ese momento, OpenGL le dice que todo lo que dibuje o configure, va a ocurrir en esta ventana.

## .glfwSwapInterval(1)
Controla la sincronización vertical (VSync) del contexto con OpenGL.
- 1 -> Activa el VSync.
- 0 -> Desactiva el VSync, la GPU renderiza tan rápido como pueda.
- Valores mayores a 1 intentan limitar más los FPS (no siempre soportado).

Este método debe llamarse después del .glfwMakeContextCurrent(window) y antes del bucle principal.

## .glfwSwapBuffers(window)
Intercambia (hace swap) entre:
- El front buffer (lo que se está mostrando en pantalla).
- El back buffer (lo que acaba de renderizar).

En otras palabras, muestra en pantalla el frame que acaba de dibujar y prepara el siguiente.
GLFW usa double buffering, por eso es necesario.
Se llama una vez por frame, normalmente al final del ciclo de renderizado.
``
```java
glfwSwapBuffers(window);
```

## .glfwPollEvents()
Procesa todos los eventos pendientes del sistema operativo, como:
- Teclas presionadas o soltadas
- Movimiento del mouse
- Clics
- Cierre de ventana
- Resize
- Eventos del sistema de ventanas (X11/Win32/Cocoa)

Importante:
- No bloquea la ejecución.
- Debe llamarse una vez por frame dentro del loop principal.

Ejemplo:
```java
while (!glfwWindowShouldClose(window)) {
	glfwPollEvents();
	// Render...
}
```

## .glfwWindowShouldClose(window)
Devuelve un booleano que indica si la ventana debería cerrarse.
Ejemplo:
```java
if (glfwWindowShouldClose(window)) {
	break; // Salir del loop
}
```

Este se activa cuando:
- El usuario presiona el botón de cerrar ventana (X)
- Manualmente se llama a:
```java
glfwSetWindowsShouldClose(window, true);
```
Se usa como condición de salida del bucle principal.

## .glfwSetKeyCallback(window, callback)
Permite asignar una función (callback) que GLFW llamará automáticamente cuando ocurra un evento de teclado.
Ejemplo:
```java
glfwSetKeyCallback(window, (windowHandle, key, scancode, action, mods) -> {
	if (key == GLFW_KEY_ESCAPE && action == GLFW_PRESS) {
		glfwSetWindowShouldClose(windowHandle, true);
	}
})
```

