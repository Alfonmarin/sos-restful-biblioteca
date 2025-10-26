# 🌐 Sistemas Orientados a Servicios – Práctica RESTful (Biblioteca)

## 🧩 Descripción general
Este proyecto corresponde a la **Primera Práctica de la asignatura Sistemas Orientados a Servicios (ETSIINF-UPM)**.  
Consiste en el diseño e implementación de un **servicio web RESTful** para la **gestión de préstamos de libros en una biblioteca**, desarrollado con **Spring Boot** y persistencia en **PostgreSQL**.

El sistema permite gestionar **usuarios, libros y préstamos** mediante operaciones CRUD, además de ofrecer funcionalidades avanzadas como:
- Ampliación y devolución de préstamos.
- Filtrado de libros por título y disponibilidad.
- Consulta de actividad e historial de cada usuario.

El servicio se complementa con un **cliente Java** que realiza pruebas automáticas sobre todos los endpoints de la API.

---

## 🎯 Objetivos principales
- Diseñar e implementar una **API RESTful completa** con Spring Boot.  
- Integrar una **base de datos relacional (PostgreSQL)** usando Spring Data JPA.  
- Aplicar principios REST: recursos, URIs, HATEOAS, paginación y códigos HTTP correctos.  
- Desarrollar un **cliente Java** para automatizar pruebas y validar la API.  
- Documentar todo el proceso, decisiones de diseño y resultados en la memoria.

---

## ⚙️ Tecnologías y herramientas
- **Lenguaje:** Java 17  
- **Framework:** Spring Boot 3.x  
- **Base de datos:** PostgreSQL  
- **Dependencias:** Spring Web, Spring Data JPA, Lombok, PostgreSQL Driver  
- **Cliente:** Java con `HttpClient` (sin interfaz gráfica)  
- **Gestor de dependencias:** Maven  
- **Pruebas:** Postman y cliente Java  
- **IDE:** IntelliJ IDEA / VS Code  

---

## 🧱 Estructura del proyecto
| Ruta / Archivo | Descripción |
|-----------------|-------------|
| **`.mvn/`, `mvnw`, `mvnw.cmd`** | Configuración y scripts de Maven Wrapper. |
| **`pom.xml`** | Archivo de dependencias y configuración de Maven. |
| **`src/main/java/com/biblioteca/`** | Código principal del servicio REST. |
| `controller/` | Controladores REST: `ContLibro`, `ContUsuario`, `ContPrestamo`. |
| `exception/` | Gestión centralizada de errores y excepciones personalizadas. |
| `model/` | Entidades JPA y DTOs (`Usuario`, `Libro`, `Prestamo`, etc.). |
| `repository/` | Interfaces JPA para acceso a la base de datos. |
| `service/` | Lógica de negocio: validaciones, filtros y reglas de préstamo. |
| **`src/main/java/cliente/ClienteBiblioteca.java`** | Cliente Java para pruebas automáticas sobre la API. |
| **`src/test/java/com/biblioteca/`** | Tests unitarios e integración. |
| **`src/main/resources/application.properties`** | Configuración de la conexión a PostgreSQL. |
| **`memoria.pdf`** | Memoria y documentación completa con el funcionamiento y pruebas. |
| **`README.md`** | Documentación principal del proyecto. |


---

## 🌐 Principales endpoints
| Método | URI | Descripción | Códigos HTTP |
|---------|-----|-------------|---------------|
| **GET** | `/usuarios` | Lista de usuarios (paginado). | 200, 400 |
| **POST** | `/usuarios` | Crea un nuevo usuario. | 201, 400 |
| **GET** | `/usuarios/{id}` | Obtiene un usuario por ID. | 200, 404 |
| **PUT** | `/usuarios/{id}` | Actualiza los datos de un usuario. | 200, 404 |
| **DELETE** | `/usuarios/{id}` | Elimina un usuario (sin préstamos activos). | 200, 400, 404 |
| **GET** | `/libros?titulo=&disponible=` | Filtra libros por título y disponibilidad. | 200, 400, 404 |
| **POST** | `/libros` | Registra un libro nuevo. | 201, 400 |
| **PUT** | `/libros/{id}` | Edita la información de un libro. | 200, 404 |
| **DELETE** | `/libros/{id}` | Elimina un libro existente. | 204, 404 |
| **POST** | `/prestamos` | Crea un préstamo (duración: 14 días). | 201, 400, 403, 404 |
| **PUT** | `/prestamos/{id}/estado` | Devuelve un préstamo. | 204, 400, 404 |
| **PUT** | `/prestamos/{id}/fecha` | Amplía el plazo de un préstamo. | 204, 400, 404 |
| **GET** | `/usuarios/{id}/prestamos` | Lista préstamos activos de un usuario. | 200, 404 |
| **GET** | `/usuarios/{id}/historial` | Consulta préstamos devueltos. | 200, 404 |
| **GET** | `/usuarios/{id}/actividad` | Muestra actividad y últimos préstamos. | 200, 404 |

---

## 🧪 Pruebas realizadas
El cliente Java ejecuta **8 pruebas automáticas (test1–test8)** que validan todos los flujos principales del sistema:
1. Crear usuario, libro y préstamo (con devolución).  
2. Alta y consulta básica de usuarios.  
3. Creación y consulta de préstamos activos.  
4. Ampliación y devolución de préstamos.  
5. Filtrado de libros por título y disponibilidad.  
6. Consulta de préstamos activos e historial.  
7. Extensión de fecha de préstamo.  
8. Consulta de actividad de usuario (resumen completo).  

Cada test comprueba los **códigos HTTP esperados**, la **consistencia de datos** y la correcta persistencia en la base de datos.
