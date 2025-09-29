- --- 
- #LenguajeDeProgramación 
- ---

# Lectura y escritura de ficheros

### *BufferedWriter y FileWriter:*

Hay que importar sus respectivas clases para utilizarlos en el código. Se utilizan para escribir en un archivo. 

Ejemplo de uso:
``` java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EjemploBufferedWriter {
    public static void main(String[] args) {
        try {
            FileWriter fw = new FileWriter("archivo.txt");
            BufferedWriter bw = new BufferedWriter(fw);

            bw.write("Hola mundo\n");
            bw.write("Segunda línea\n");

            bw.close(); // Cierra el buffer y también el FileWriter subyacente
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```


### *BufferedReader y FileReader:*

Hay que importar sus respectivas clases para utilizarlos en el código. Se utilizan para abrir un archivo y leer su contenido.

Ejemplo de uso:
``` java
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;

public class LeerArchivo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("archivo.txt"))) {
            String linea;
            while ((linea = br.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```


# Comparadores
### *Comparator:*

Se utiliza para ordenar clases según unos atributos establecidos.

Ejemplo:

***Clase Persona***
``` java
import java.util.*;

public class Persona {
    String nombre;
    int edad;

    Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```

***Clase ComparadorPorEdad***
``` java
import java.util.*;

 public class ComparadorPorEdad implements Comparator<Persona> {
    @Override
    public int compare(Persona p1, Persona p2) {
        return p1.edad - p2.edad;
    }
}
```

***Clase Principal***
``` java
import java.util.*;

public class EjemploComparator {
    public static void main(String[] args) {
        List<Persona> lista = Arrays.asList(
            new Persona("Ana", 25),
            new Persona("Luis", 30),
            new Persona("Maria", 20)
        );

        Collections.sort(lista, new ComparadorPorEdad());

        for (Persona p : lista) {
            System.out.println(p.nombre + " - " + p.edad);
        }
    }
}
```


### *Comparable*

Sirve para **definir el orden natural de los objetos de una clase**, de manera que puedan ser **ordenados automáticamente** con `Collections.sort()` o `List.sort()`.

Ejemplo:

``` java
import java.util.*;

class Persona implements Comparable<Persona> {
    String nombre;
    int edad;

    Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    @Override
    public int compareTo(Persona otra) {
        return this.edad - otra.edad;
    }
}

public class EjemploComparable {
    public static void main(String[] args) {
        List<Persona> lista = Arrays.asList(
            new Persona("Ana", 25),
            new Persona("Luis", 30),
            new Persona("Maria", 20)
        );

        Collections.sort(lista);

        for (Persona p : lista) {
            System.out.println(p.nombre + " - " + p.edad);
        }
    }
}

```