- ---
- Tags: #Personal #LenguajeDeProgramación #Java #Librería
- --
# Iniciar OpenGL
## GL.createCapabilities()
Inicializa todas las funciones de OpenGL para LWJGL.
Después de hacer glfwMakeContextCurrent(window) necesitas llamar a:
```java
GL.createCapabilities();
```

Esto:
- Carga todas las funciones nativas de OpenGL desde el driver.
- Permite usar métodos como glClearColor, glBegin, glVertex, VBOs, shaders, etc.
- Debe llamarse una sola vez por contexto.
Sin esto ninguna llamada a OpenGL funcionará.

## .glClearColor(r, g, b, a)
Define el color con el que se borrará la pantalla cuando llames a glClear().
Los parámetros:
- r, g, b, a -> Valores entre 0.0 y 1.0
Ejemplo:
```java
glClearColor(0f, 0f, 0f, 1f);
```

## .glClear(GL_COLOR_BUFFER_BIT)
Limpia el buffer de color usando el color definido en glClearColor()

Es básicamente:
Pintar toda la pantalla del color de fondo.
Se usa al comienzo de cada frame antes del dibujo.

Ejemplo:
```java
glClear(GL_COLOR_BUFFER_BIT);
```

# Dibujar primitivas
> [!WARNING] Importante: 
> Estas funciones pertenecen a OpenGL antiguo (Fixed Pipeline / Inmediate Mode).
Son fáciles para aprender, pero están obsoletas para produción moderna.

## .glBegin(GL_QUADS)
Indica el inicio del dibujo de una primitiva.
Ejemplo: GL_QUADS dibuja cuadrilateros (4 vertices por figura).
```java
glBegin(GL_QUADS);
```
Dentro del glBegin -> defines vértices con gVertex*.

## .glVertex2f(x, y)
Define un vértice 2D con coordenadas x e y.
Ejemplo dentro de un quad:
```java
glBegin(GL_QUADS);
glVertex2f(0, 0);
glVertex2f(100, 0);
glVertex2f(100, 100);
glVertex2f(0, 100);
glEnd();
```
Se dibujan en el orden en que se declaren.
## .glEnd()
Indica qu eterminaste de definir la primitiva que comenzó con glBegin.

# Transformaciones básicas
## .glPushMatrix()


## .glPopMatrix()


## .glTransalatef()


## .glRotatef()


## .glScalef()



# Establecer modo ortográfico
## .glMatrixMode(GL_PROJECTION)


## .glLoadIdentity()


## .glOrtho(0, width heigth, 0, -1, 1)


