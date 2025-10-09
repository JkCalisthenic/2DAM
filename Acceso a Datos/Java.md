
Ejemplo básico que contiene RandomAccessFile para la escritura de ficheros en binario y de StringBuffer para ajustar el tamaño de un String:
``` java
package EjercicioBinario;

import java.io.IOException;
import java.io.RandomAccessFile;

public class Principal {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        populateGummies();
    }

    public static void populateGummies() {
        Integer[] shelfs = {3, 2, 3, 8, 1};
        String[] gummies = {"Chicles", "Gusanitos", "Gominola", "Pipas", "Piruletas"};
        Double[] costs = {3.2, 18.5, 2.5, 15.17, 12.40};

        try {
            RandomAccessFile raf = new RandomAccessFile("quiosco.dat", "rw");

            for (int i = 0; i < shelfs.length; i++) {
                raf.writeInt(i + 1); // ID del producto
                raf.writeInt(shelfs[i]); // Número de estantería

                // Convertimos el nombre a una cadena fija de 20 caracteres
                StringBuffer sB = new StringBuffer(gummies[i]);
                sB.setLength(20);
                raf.writeChars(sB.toString());

                raf.writeDouble(costs[i]); // Precio
            }

            raf.close();
            System.out.println("Archivo 'quiosco.dat' creado correctamente.");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```