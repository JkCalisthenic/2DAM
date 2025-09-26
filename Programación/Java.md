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


