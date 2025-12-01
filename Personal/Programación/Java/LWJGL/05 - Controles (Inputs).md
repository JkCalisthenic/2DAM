- ---
- Tags: #Personal #LenguajeDeProgramación #Java #Librería
- --
# Métodos
## GLFW.glfwGetKey(window, GLFW_KEY_...)
Este método permite consultar el estado actual de una tecla en cualquier momento del bucle principal.

Su uso típico es:
```java
int state = gelfwGetKey(window, GLFW_KEY_W);
```
Devuelve uno de dos valores:
- GLFW_PRESS -> la tecla está presionada
- FLFW_RELEASE -> la tecla está soltada

Sirve para comprobación continua en lugar de usar callbacks.
Ejemplo:
```java
if (glfwGetKey(window, GLFW_KEY_SPACE) == GLFW_PRESS) {
	// Saltar
}
```
## GLFW_PRESS
Constante que indica que la tecla está presionada.
Valor devuelto por:
- glfwGetKey
- Key callbacks (glfwSetKeyCallback)
- Eventos de teclado en general

También se usa para detectar evento de pulsación directa dentro del callback.

Ejemplo:
```java
if (action == GLFW_PRESS) {
    // La tecla se acaba de presionar
}
```

## GLFW RELEASE
Constante que indica que la tecla está **soltada**.

Se usa para detectar:
- que el usuario dejó de presionar la tecla
- el fin de una interacción

También aparece en callbacks:
```java
if (action == GLFW_RELEASE) {
    // La tecla se soltó
}
```
