# Estudiante: Angela Arcos
# Carrera: Desarrollo de Software

# 🚀 Proyecto Final: Frontend - Consumo de Microservicios Distribuidos

## 🛠️ Framework y Herramientas Utilizadas
Para el desarrollo de la interfaz de usuario se seleccionó **React.js**, una de las librerías de JavaScript más robustas para la creación de Single Page Applications (SPA).

- **Framework**: React 18+
- **Lenguaje**: JavaScript (ES6+)
- **Estilos**: CSS3 Personalizado (Tema Universitario Japón)
- **Consumo de API**: Fetch API / Promesas
- **Entorno de Ejecución**: Node.js & Docker Desktop

## 📝 Descripción del Proyecto
Este proyecto representa la capa de presentación (Frontend) de una arquitectura basada en microservicios. Su objetivo principal es permitir que un usuario final gestione registros de clientes de forma visual, abstrayendo la complejidad de las peticiones HTTP y la comunicación con la base de datos PostgreSQL que reside en contenedores independientes.

## 🔗 APIs y Endpoints Consumidos
El frontend se comunica con el microservicio de facturación/clientes a través de un **API Gateway** simulado por el puerto **8080** de Docker:

| Acción | Método | Endpoint | Descripción |
| :--- | :--- | :--- | :--- |
| **Listar** | GET | `/api/persona` | Obtiene todos los registros desde PostgreSQL. |
| **Crear** | POST | `/api/persona` | Envía un objeto JSON para persistir un nuevo cliente. |
| **Editar** | PUT | `/api/persona/{id}` | Actualiza la información de un registro existente. |
| **Eliminar**| DELETE| `/api/persona/{id}` | Remueve un registro de forma lógica/física. |

##  Explicación Técnica: Consumo de APIs
El consumo se realiza de forma asíncrona para no bloquear el hilo principal de la aplicación. Se utiliza el hook `useEffect` para disparar la carga de datos apenas el componente se monta en el DOM.

### Fragmento de Código Principal:
```javascript
const API_URL = "http://localhost:8080/api/persona";

// Función asíncrona para obtener datos (GET)
async function cargarDatos() {
    try {
        const respuesta = await fetch(API_URL);
        if (!respuesta.ok) throw new Error("Status: " + respuesta.status);
        const json = await respuesta.json();
        setDatos(json);
    } catch (err) {
        console.error("Fallo en la conexión con el microservicio:", err);
    }
}
