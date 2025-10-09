
Ejemplo básico que contiene RandomAccessFile para la escritura de ficheros en binario y de StringBuffer para ajustar el tamaño de un String:
``` java
package EjercicioBinario;

import java.io.IOException;
import java.io.RandomAccessFile;

public class Principal {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        populateGummies();
        leerFichero();
    }

    public static void populateGummies() {
        Integer[] shelfs = {3, 2, 3, 8, 1};
        String[] gummies = {"Chicles", "Gusanitos", "Gominola", "Pipas", "Piruletas"};
        Double[] costs = {3.2, 18.5, 2.5, 15.17, 12.40};

        try {
            RandomAccessFile raf = new RandomAccessFile(
                "C:\\Users\\ferna\\eclipse-workspace\\acceso_a_datos\\src\\EjercicioBinario\\quiosco.dat",
                "rw"
            );

            for (int i = 0; i < shelfs.length; i++) {
                raf.writeInt(i + 1);
                raf.writeInt(shelfs[i]);
                StringBuffer sB = new StringBuffer(gummies[i]);
                sB.setLength(20);
                raf.writeChars(sB.toString());
                raf.writeDouble(costs[i]);
            }

            raf.close();

        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

    public static void leerFichero() {

        // 4 + 4 + 20*2 + 8 = 56

        Integer id;
        Integer shelf;
        String gummie;
        Double cost;

        try {
            RandomAccessFile raf = new RandomAccessFile(
                "C:\\Users\\ferna\\eclipse-workspace\\acceso_a_datos\\src\\EjercicioBinario\\quiosco.dat",
                "rw"
            );

            for (int i = 0; i < (raf.length() / 56); i++) {
                id = raf.readInt();
                shelf = raf.readInt();

                gummie = "";
                for (int j = 0; j < 20; j++) {
                    gummie += raf.readChar();
                }

                cost = raf.readDouble();

                System.out.println(id + " - " + shelf + " - " + gummie.trim() + " - " + cost);
            }

            raf.close();

        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }

    }

}


```

