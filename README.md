```text
███████╗ █████╗ ███████╗████████╗ █████╗ ██████╗ ██╗
██╔════╝██╔══██╗██╔════╝╚══██╔══╝██╔══██╗██╔══██╗██║
█████╗  ███████║███████╗   ██║   ███████║██████╔╝██║
██╔══╝  ██╔══██║╚════██║   ██║   ██╔══██║██╔═══╝ ██║
██║     ██║  ██║███████║   ██║   ██║  ██║██║     ██║
╚═╝     ╚═╝  ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝     ╚═╝
```

# Sistema de Registro de Aprendices SENA

> API REST desarrollada con **FastAPI** y **MongoDB Atlas** para la gestión integral de aprendices del SENA, con interfaz interactiva en consola (**CLI**) y despliegue en la nube.

🔗 **Enlaces de Despliegue:**
- 🌐 **API en Producción (Render):** [https://fastapi-erk0.onrender.com/](https://fastapi-erk0.onrender.com/)
- 📄 **Documentación Interactiva (Swagger UI):** [https://fastapi-erk0.onrender.com/docs](https://fastapi-erk0.onrender.com/docs)

## 📘 Título y Descripción

### Información del Aprendiz
- **Nombre:** Joan Stiven  
- **Ficha:** 3494620  
- **Competencias:**
  - Elaboración de la propuesta técnica para la solución de software.
  - Implantación del software.

### Descripción del Proyecto
Proyecto formativo en Python orientado a la gestión de datos de aprendices SENA. Implementa una arquitectura en capas, persistencia de datos en la nube con MongoDB Atlas, validaciones estrictas de esquemas con Pydantic y una interfaz CLI intuitiva que consume los endpoints mediante peticiones HTTP asíncronas con HTTPX.

### Datos del Aprendiz Gestionados
Cada registro almacena la siguiente información:
* **Documento:** Documento de identidad del aprendiz.
* **Nombres:** Nombres completos.
* **Apellidos:** Apellidos completos.
* **Correo:** Correo electrónico institucional o personal (validado).
* **Edad:** Edad del aprendiz.
* **Programa:** Nombre del programa de formación.
* **Ficha:** Número de ficha asociada.

## 🛠️ Herramientas Utilizadas

* **Python 3.10+**: Lenguaje principal de desarrollo.
* **FastAPI**: Framework web moderno y de alto rendimiento para la construcción de la API REST.
* **Uvicorn**: Servidor ASGI de alto rendimiento para ejecutar la aplicación.
* **MongoDB Atlas & PyMongo**: Base de datos NoSQL en la nube y su cliente oficial en Python.
* **Pydantic**: Validación de datos y tipado estricto (`BaseModel`, `EmailStr`).
* **HTTPX**: Cliente HTTP moderno utilizado en la vista de consola para interactuar con la API.
* **Python-dotenv**: Gestión segura de variables de entorno y credenciales sensibles.
* **Render**: Plataforma de nube utilizada para el despliegue en producción.

## 🗂️ Estructura del Proyecto

```text
fastapi/
│
├── src/
│   ├── main.py                # Punto de entrada de la aplicación y rutas de la API
│   │
│   ├── controllers.py         # Capa CONTROLLER: Lógica de negocio y operaciones con la base de datos
│   │
│   ├── models/                # Capa MODEL: Esquemas de Pydantic y lógica de persistencia
│   │   ├── database.py        # Configuración y conexión con MongoDB Atlas
│   │   └── model.py           # Esquemas de datos (TraineeModel y TraineeUpdateModel)
│   │
│   ├── views/                 # Capa VIEW: Interfaz en consola (CLI) para consumo de la API
│   │   └── view.py            # Menú interactivo y consumo de endpoints mediante HTTPX
│   │
│   └── templates/             # Capa TEMPLATE: Plantillas y formatos de salida
│
├── data/                      # Almacenamiento y persistencia de datos locales
│
├── test/
│   └── test_main.py           # Pruebas de conexión e inserción en MongoDB
│
├── .env                       # Variables de entorno protegidas (MONGO_URL, BASE_URL)
├── .env.example               # Plantilla de variables de entorno requeridas
├── .gitignore                 # Archivos y directorios ignorados por Git
├── README.md                  # Documentación del proyecto
├── requirements.txt           # Dependencias del proyecto
└── structure.sh               # Script de creación de la estructura de carpetas
```

## 📡 Endpoints de la API

| Método | Endpoint | Descripción |
| :--- | :--- | :--- |
| `GET` | `/` | Comprobación del estado del servicio (*Health check*) |
| `POST` | `/trainees` | Registrar un nuevo aprendiz |
| `GET` | `/trainees` | Obtener la lista de todos los aprendices |
| `GET` | `/trainees/{trainee_id}` | Obtener un aprendiz por su ID (`_id` de MongoDB) |
| `PUT` | `/trainees/{trainee_id}` | Actualizar parcialmente los datos de un aprendiz |
| `DELETE` | `/trainees/{trainee_id}` | Eliminar un aprendiz por su ID |

## 🚀 Instalación y Ejecución

### 1. Clonar el repositorio
```bash
git clone https://github.com/srjoans/fastapi.git
cd fastapi
```

### 2. Crear y activar el entorno virtual
```bash
# Linux / macOS
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 4. Configurar variables de entorno
Crea tu archivo `.env` a partir de la plantilla `.env.example`:
```bash
cp .env.example .env
```

Configura tus credenciales en el archivo `.env`:
```env
MONGO_URL=mongodb+srv://<usuario>:<password>@<cluster>.mongodb.net/
BASE_URL=https://fastapi-erk0.onrender.com/
```

> [!NOTE]
> Si deseas probar la interfaz CLI apuntando a tu servidor local en vez de Render, cambia `BASE_URL` por `http://127.0.0.1:8000`.

### 5. Iniciar el Servidor de la API (Modo local)
```bash
uvicorn src.main:app --reload
```
La API estará disponible en `http://127.0.0.1:8000` y la documentación interactiva en `http://127.0.0.1:8000/docs`.

### 6. Ejecutar la Interfaz en Consola (CLI)
En otra terminal (con el entorno virtual activado):
```bash
python3 src/views/view.py
```
