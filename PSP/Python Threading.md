- --
- Tags: #Python #Clase #PSP #LenguajeDeProgramación 
- --
El módulo `threading` de Python permite ejecutar múltiples hilos (threads) de forma concurrente dentro del mismo proceso, compartiendo memoria pero ejecutándose en paralelo (limitado por el GIL, aunque útil para tareas I/O).
# Hilos (Threads)
Un **hilo** es una secuencia de ejecución independiente dentro de un programa.  
Permiten realizar tareas simultáneas, como descargar archivos, procesar datos y responder a la interfaz al mismo tiempo.

**Ejemplo básico:**
```python
import threading

def tarea():
    print("Ejecutando hilo")

hilo = threading.Thread(target=tarea)
hilo.start()
hilo.join()
```
🔹 `start()` → inicia el hilo.  
🔹 `join()` → espera a que el hilo termine antes de continuar.

# Lock (Bloqueo)
Un **Lock** impide que varios hilos accedan simultáneamente a una sección crítica del código (por ejemplo, una variable compartida).

**Ejemplo:**
```python
import threading

contador = 0
lock = threading.Lock()

def incrementar():
    global contador
    for _ in range(100000):
        with lock:  # Bloquea la sección crítica
            contador += 1

t1 = threading.Thread(target=incrementar)
t2 = threading.Thread(target=incrementar)

t1.start(); t2.start()
t1.join(); t2.join()

print(contador)
```
🔹 `lock.acquire()` y `lock.release()` → bloquean y liberan manualmente.  
🔹 `with lock:` → usa el bloqueo automáticamente.

```python
import threading

contador = 0
lock = threading.Lock()

def incrementar():
    global contador
    for _ in range(100000):
        lock.acquire()   # Bloquea la sección crítica
        try:
            contador += 1
        finally:
            lock.release()  # Libera el bloqueo, incluso si ocurre un error

t1 = threading.Thread(target=incrementar)
t2 = threading.Thread(target=incrementar)

t1.start()
t2.start()

t1.join()
t2.join()

print(contador)
```
## Explicación:
- `lock.acquire()` bloquea el acceso de otros hilos a la sección crítica.
- `try...finally` garantiza que el `lock` siempre se libere, **incluso si ocurre una excepción** dentro del bloque.
- `lock.release()` libera el bloqueo, permitiendo que otro hilo entre a la sección crítica.

El resultado será **200000**, ya que el `Lock` evita que ambos hilos modifiquen `contador` al mismo tiempo.

# Semaphore (Semáforo)
Un **semáforo** controla el número de hilos que pueden acceder a un recurso al mismo tiempo.

**Ejemplo:**
```python
import threading
import time

semaforo = threading.Semaphore(3)

def tarea(num):
    with semaforo:
        print(f"Hilo {num} trabajando...")
        time.sleep(1)
        print(f"Hilo {num} terminó")

for i in range(6):
    threading.Thread(target=tarea, args=(i,)).start()
```
🔹 Solo **3 hilos** podrán ejecutar la sección crítica simultáneamente.

# Event (Evento)
Un **Event** permite que un hilo espere hasta que otro hilo emita una señal.

**Ejemplo:**
```python
import threading
import time

evento = threading.Event()

def esperar():
    print("Esperando señal...")
    evento.wait()
    print("¡Señal recibida!")

def emitir():
    time.sleep(2)
    evento.set()

threading.Thread(target=esperar).start()
threading.Thread(target=emitir).start()
```
🔹 `wait()` → el hilo se bloquea hasta que se llama a `set()`.  
🔹 `clear()` → reinicia el evento.

# Barrier (Barrera)
Una **barrera** sincroniza un conjunto de hilos, haciendo que todos esperen hasta que todos hayan llegado a un punto común.

**Ejemplo:**
```python
import threading
import time

barrera = threading.Barrier(3)

def tarea(num):
    print(f"Hilo {num} esperando...")
    barrera.wait()
    print(f"Hilo {num} continúa")

for i in range(3):
    threading.Thread(target=tarea, args=(i,)).start()
```
🔹 Todos los hilos deben llegar a la barrera antes de continuar.  
🔹 Se usa en simulaciones o sincronización de etapas.
# Condition (Condición)
Una **Condition** permite que los hilos esperen una señal específica, y que otros hilos notifiquen cuando deben continuar.

**Ejemplo:**
``` python
import threading

cond = threading.Condition()
lista = []

def productor():
    with cond:
        lista.append("dato")
        print("Productor: dato añadido")
        cond.notify()  # Despierta al consumidor

def consumidor():
    with cond:
        print("Consumidor esperando dato...")
        cond.wait()
        print("Consumidor: dato recibido:", lista.pop())

threading.Thread(target=consumidor).start()
threading.Thread(target=productor).start()
```
🔹 `wait()` → suspende el hilo hasta `notify()` o `notify_all()`.  
🔹 Ideal para patrones **productor-consumidor**.
