- ---
- Tags: #Personal #LenguajeDeProgramación #Java #Librería
- --
Para la creación de un proyecto con esta librería, al no ser un .jar y ser una configuración hay que hacer un maven proyect

# Creación de un Maven Proyect
Esta es la primera pantalla en la que marcaremos solo Create a simple project y le daremos a next
![[image.png]]

En la segunda pantalla rellenaremos los siguientes campos y una vez hecho le daremos a finish
![[image-1.png]]

Si todo se ha hecho de forma correcta se nos creará un proyecto con la siguiente arquitectura:
![[image-2.png]]
# Configuración del pom.xml
En caso del siguiente error:
![[image-3.png]]

Iremos a Windows -> Preferences -> XML y activaremos la opción de Download externasl resources...
![[image.png]]

Una vez hecho esto, se eliminará el error y deberemos agregar las dependencias a nuestro pom.xml, quedando de la siguiente manera:
``` xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">

<modelVersion>4.0.0</modelVersion>

<groupId>com.jk.games</groupId>

<artifactId>lwjgl-test</artifactId>

<version>0.0.1-SNAPSHOT</version>

<dependencies>

<!-- LWJGL Core -->

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl</artifactId>

<version>3.3.3</version>

</dependency>

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl</artifactId>

<version>3.3.3</version>

<classifier>natives-windows</classifier>

</dependency>

  

<!-- GLFW -->

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl-glfw</artifactId>

<version>3.3.3</version>

</dependency>

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl-glfw</artifactId>

<version>3.3.3</version>

<classifier>natives-windows</classifier>

</dependency>

  

<!-- OpenGL -->

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl-opengl</artifactId>

<version>3.3.3</version>

</dependency>

<dependency>

<groupId>org.lwjgl</groupId>

<artifactId>lwjgl-opengl</artifactId>

<version>3.3.3</version>

<classifier>natives-windows</classifier>

</dependency>

  

</dependencies>

  

</project>
```


