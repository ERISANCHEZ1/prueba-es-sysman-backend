# Task Manager - Backend Java

Este backend proporciona una API RESTful para gestionar tareas (crear, consultar, actualizar y eliminar). Está construido en Java con Servlets y se conecta a una base de datos Oracle mediante JDBC.

---

## 🛠️ Tecnologías utilizadas

- Java 17
- Jakarta Servlet API (v6.0)
- Apache Tomcat 10
- JDBC
- Oracle Database
- Gson (para serialización/deserialización JSON)
- Maven (gestión de dependencias)

---

## 📁 Estructura del proyecto

task-manager-backend/
│
├── src/main/java/com/erika/tasks/
│ ├── dao/TaskDAO.java # Lógica de acceso a datos
│ ├── model/Task.java # POJO que representa una tarea
│ └── servlet/TaskServlet.java # Servlet principal que expone los endpoints REST
│
├── webapp/
│ └── WEB-INF/web.xml # Configuración del servlet (opcional con anotaciones)
│
├── pom.xml # Dependencias y configuración de compilación
└── README.md # Documentación del backend

---

## 🌐 Endpoints expuestos

### Base URL:
http://localhost:8082/task-manager-backend/api/tasks


### 1. Obtener todas las tareas
`GET /api/tasks`

- **Descripción:** Devuelve la lista de tareas registradas.
- **Respuesta:** JSON array de tareas

---

### 2. Crear una nueva tarea  
`POST /api/tasks`

- **Body JSON:**
```json
{
  "title": "Ejemplo de tarea",
  "description": "Descripción opcional",
  "completed": false
}
Respuesta:

{ "success": true }

3. Actualizar tarea
PUT /api/tasks

Body JSON:

{
  "task_id": 1,
  "title": "Título actualizado",
  "description": "Nueva descripción",
  "completed": true
}
Respuesta:

{ "success": true }

4. Eliminar tarea
DELETE /api/tasks/{id}

Ejemplo: DELETE /api/tasks/5

Respuesta:
{ "success": true }

⚙️ Configuración de base de datos
La conexión JDBC se realiza en TaskDAO.java. Asegúrate de modificar las credenciales:

private static final String DB_URL = "jdbc:oracle:thin:@localhost:1521:xe";
private static final String DB_USER = "tu_usuario";
private static final String DB_PASSWORD = "tu_contraseña";

🔄 Ciclo de vida de las operaciones

📌 POST
Recibe un JSON desde Angular o Postman.

Lo convierte en un objeto Task usando Gson.

Llama a createTask() en TaskDAO y lo inserta en Oracle.

📌 PUT
Igual al POST, pero ejecuta un UPDATE por task_id.

📌 DELETE
Obtiene el ID desde la URL (/api/tasks/{id}).

Llama a deleteTask(id) y elimina el registro.

🧪 Pruebas
Se probaron todos los endpoints con Postman y el frontend en Angular.

Se validó el manejo de errores y la respuesta en formato JSON.


🚀 Cómo ejecutar el backend
Clonar el repositorio.

Configurar DB_URL, DB_USER y DB_PASSWORD en TaskDAO.java.

Asegurarse de tener Tomcat configurado y en ejecución.

Usar mvn clean package para compilar y desplegar en Tomcat.

Acceder a los endpoints vía navegador, Postman o Angular frontend.

📝 Dependencias principales en pom.xml

<dependencies>
  <dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10</version>
  </dependency>
  <dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>6.0.0</version>
    <scope>provided</scope>
  </dependency>
</dependencies>

El manejo de CORS está habilitado en el servlet para desarrollo local.
