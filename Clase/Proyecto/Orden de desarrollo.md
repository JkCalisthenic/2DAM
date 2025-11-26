- --
- Tags: #Clase #Proyecto 
- --
- [ ] **Definir las pantallas y mockups del frontend**  
    - [ ] **Pantallas generales**
	    - [ ] Pantalla de inicio / login
		    - [ ] Selección del tipo de cuenta: Administrativa / Docente / Alumno
		    - [ ] Opción de iniciar sesión:
			    - [ ] Administradores: usuario y contrasñ
			    - [ ] Docentes: token, qr, usuario y contraseña 
			    - [ ] Alumnos: token o qr, sin usuario ni contraseña 
	    - [ ] Pantalla de activación (solo la primera vez)
		    - [ ] Introducción del token o escaneo de QR
	
    - [ ] **Pantallas para alumnos**
	    - [ ] Menú principal
		    - [ ] Enviar mensaje 
		    - [ ] Ver mural / mensajes públicos 
		    - [ ] Enviar mensaje privado (bullyng / casos delicados)
	    - [ ] Pantalla de envío de mensajes
		    - [ ] Selección: público / privado
		    - [ ] Campos (título / tema / curso / descripción)
		    - [ ] Pop up de advertencia de ser respetuoso antes de mandar el mensaje 
	    - [ ] Pantalla mural público
		    - [ ] Lista de mensajes en tarjeta
		    - [ ] En cada publicación agregar vote y unbote con comentarios
	    - [ ] Pantalla de mensajes privados (para bulling y casos delicados)
		    - [ ] Mensajes de advertencia y apoyo
		    - [ ] Formulario idéntico al de mensajes públicos 
	
    - [ ] **Pantallas para docentes**
	    - [ ] Manú principal
	    - [ ] Panel de mensajes públicos
	    - [ ] Panel de mensajes privados
	    - [ ] Pantalla de perfil y ajustes
	
	- [ ] **Pantallas para administrador / centro**
		- [ ] Panel de control del centro
		- [ ] Gestión de tokens y códigos QR
		- [ ] Panel de configuración de IA

- [ ] **Diseñar la base de datos completa**
    - [ ] Tablas
    - [ ] Relaciones
    - [ ] Campos
    - [ ] Tipos de datos

- [ ] **Crear el backend en Java (Spring Boot)**
    - [ ] Conectar a MySQL
    - [ ] Crear entidades
    - [ ] Crear repositorios
    - [ ] Crear servicios
    - [ ] Crear controladores REST
    - [ ] Probar la API con Postman

- [ ] **Desarrollar el frontend (React Native y React Web)**
    - [ ] Crear pantallas
    - [ ] Implementar navegación
    - [ ] Conectar con la API del backend
    - [ ] Manejar estado y lógica visual

- [ ] **Unir frontend + backend**
    - Peticiones reales
    - [ ] Autenticación
    - [ ] CRUD de datos
    - [ ] Validaciones

- [ ] **Implementar toda la funcionalidad completa**
    - [ ] Lógica de mensajes
    - [ ] Roles
    - [ ] Sistema de reportes
    - [ ] Sistema anónimo
    - [ ] Todo lo que tu app necesite

- [ ] **Pruebas completas**
    - [ ] En móviles (Android/iOS)
    - [ ] En web
    - [ ] En API
    - [ ] Base de datos

- [ ] **Despliegue (publicación)**
    - [ ] Backend → Render, Railway, AWS
    - [ ] BD → MySQL en la nube
    - [ ] Web → Vercel
    - [ ] Móvil → Play Store y App Store
