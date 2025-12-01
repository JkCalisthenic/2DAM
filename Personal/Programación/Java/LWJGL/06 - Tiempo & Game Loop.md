- ---
- Tags: #Personal #LenguajeDeProgramación #Java #Librería
- --

# GLFW.glfw.GetTime()
Devuelve el tiempo en segundos desde que se inició GLFW con glfwInit().
Sirve para:
- Medir intervalos de tiempo
- Calcular delta time
- Hacer animaciones suaves
- Sincronizar lógica
- Medir FPS
Ejemplo básico:
```java
double parentTime = glfwGetTime();
```

## Fórmulas típicas:
### Delta time
El delta time es la cantidad de tiempo que pasa entre un frame y el siguiente.
```java
double currentTime = glfwGetTime();
double delta = currentTime - lastTime;
lastTime = currentTime;
```
delta se usa para animaciones suaves usando tiempo real en lugar de FPS.

### Movimiento basado en delta
Permite que un objeto se mueva a la misma velocidad sin importar los FPS.
```java
x += speed * delta; // movimiento uniforme
```
Donde:
- speed -> Unides por segundo.
- delta -> segundos transcurridos entre frames.

### FPS lock (60FPS)
Un FPS lock básico (no recomendado para producción, pero útil para aprendizaje):
```java
double frameStart = glfwGetTime();
double frameDuration = 1.0 / 60.0; // 60 FPS

while (glfwGetTime() - frameStart < frameDuration) {
    // esperar
}
```
Sin embargo, lo recomendable es usar:
- glfwSwapInterval(1) -> VSync
- O un sistema de temporizador más preciso