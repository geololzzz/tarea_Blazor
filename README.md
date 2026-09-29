# 🌸 Programación II — Clientes Blazor

# 💗 Sistema de Gestión de Clientes

### Blazor WebAssembly · .NET 10 · REST API

![.NET](https://img.shields.io/badge/.NET-10.0-ec4899?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor](https://img.shields.io/badge/Blazor-WebAssembly-f472b6?style=for-the-badge&logo=blazor&logoColor=white)
![C%23](https://img.shields.io/badge/C%23-CSharp-db2777?style=for-the-badge&logo=csharp&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5-f9a8d4?style=for-the-badge&logo=bootstrap&logoColor=white)

### 🌷 Proyecto académico de Programación II

**Desarrollado por:**  
**Sharon Georgette Nahomy Calancho Toledo**

---

## 🌸 Descripción del proyecto

Este proyecto consiste en una aplicación web desarrollada con **Blazor WebAssembly sobre .NET 10**, orientada a la administración de clientes mediante operaciones **CRUD**.

La aplicación Blazor funciona como **frontend** y consume una **API REST desarrollada con ASP.NET Core**.

La aplicación **no accede directamente a la base de datos**. Toda la comunicación con los datos se realiza a través de la API utilizando peticiones HTTP y objetos JSON.

---

## 💗 Arquitectura del sistema

La aplicación utiliza una arquitectura donde el frontend se encuentra separado del acceso y procesamiento de los datos.

```text
┌─────────────────────────────┐
│     Blazor WebAssembly      │
│          Frontend           │
└──────────────┬──────────────┘
               │
               │ HTTP / JSON
               ▼
┌─────────────────────────────┐
│      ASP.NET Core API       │
│   Programacion2ClientesAPI  │
└──────────────┬──────────────┘
               │
               │ Entity Framework Core
               ▼
┌─────────────────────────────┐
│            MySQL            │
│       Base de Datos         │
└─────────────────────────────┘
```

### 🌷 Flujo de comunicación

```text
Usuario
   ↓
Blazor WebAssembly
   ↓
ClienteService
   ↓
HttpClient
   ↓
API REST
   ↓
ASP.NET Core
   ↓
Entity Framework Core
   ↓
MySQL
```

---

## 🌷 Tecnologías utilizadas

| Tecnología             | Uso                        |
| ---------------------- | -------------------------- |
| **.NET 10**            | Plataforma principal       |
| **Blazor WebAssembly** | Desarrollo del frontend    |
| **C#**                 | Lenguaje de programación   |
| **ASP.NET Core**       | Desarrollo de la API REST  |
| **Bootstrap**          | Diseño de la interfaz      |
| **HttpClient**         | Comunicación con la API    |
| **JSON**               | Intercambio de información |
| **DataAnnotations**    | Validación de modelos      |
| **MySQL**              | Base de datos              |
| **Git**                | Control de versiones       |
| **GitHub**             | Repositorio del proyecto   |

---

## 💕 Funcionalidades

El módulo de clientes permite realizar las principales operaciones de un sistema CRUD:

- 🌸 **Listar clientes**
- 💗 **Registrar nuevos clientes**
- 🌷 **Editar clientes existentes**
- 🩷 **Eliminar clientes**
- 🔄 **Actualizar automáticamente el listado**
- ✨ **Mostrar mensajes de éxito o error**
- 📝 **Validar los datos ingresados**
- 🪟 **Utilizar ventanas modales para las operaciones**

---

## 🌸 Estructura del proyecto

```text
Programacion2ClientesBlazor/
│
├── Layout/
│
├── Models/
│   └── Cliente.cs
│
├── Pages/
│   └── Clientes.razor
│
├── Services/
│   └── ClienteService.cs
│
├── wwwroot/
│
├── App.razor
├── Program.cs
├── _Imports.razor
├── Programacion2ClientesBlazor.csproj
│
└── README.md
```

---

## 💗 Comunicación con la API

La aplicación utiliza `HttpClient` para comunicarse con el backend.

El servicio principal encargado de esta comunicación se encuentra en:

```text
Services/ClienteService.cs
```

La dirección base de la API se configura desde:

```text
Program.cs
```

Ejemplo:

```csharp
builder.Services.AddScoped(sp =>
    new HttpClient
    {
        BaseAddress = new Uri("http://localhost:5169/")
    });
```

> 🌷 **Importante:** el puerto configurado en Blazor debe coincidir con el puerto utilizado al ejecutar `Programacion2ClientesAPI`.

---

## 🌸 Endpoints utilizados

|  Método  | Endpoint             | Operación             |
| :------: | -------------------- | --------------------- |
|  `GET`   | `/api/clientes`      | Listar clientes       |
|  `GET`   | `/api/clientes/{id}` | Obtener un cliente    |
|  `POST`  | `/api/clientes`      | Crear un cliente      |
|  `PUT`   | `/api/clientes/{id}` | Actualizar un cliente |
| `DELETE` | `/api/clientes/{id}` | Eliminar un cliente   |

---

# 💕 Ejecución del proyecto

## 1️⃣ Ejecutar la API

Primero debe estar funcionando el proyecto:

```text
Programacion2ClientesAPI
```

Desde la terminal:

```bash
dotnet run
```

Por ejemplo, la API puede ejecutarse en:

```text
http://localhost:5169
```

---

## 2️⃣ Ejecutar Blazor

Ingresar a la carpeta del proyecto:

```bash
cd Programacion2ClientesBlazor
```

Restaurar las dependencias:

```bash
dotnet restore
```

Ejecutar la aplicación:

```bash
dotnet run
```

Posteriormente, abrir en el navegador la dirección indicada por la consola.

Por ejemplo:

```text
http://localhost:5122
```

Para acceder directamente al módulo de clientes:

```text
http://localhost:5122/clientes
```

---

# 🌷 Operaciones CRUD

## 💗 Crear

El usuario ingresa los datos correspondientes en el formulario de clientes.

Blazor realiza una petición:

```http
POST /api/clientes
```

La API recibe y valida la información antes de registrar el cliente en MySQL.

---

## 🌸 Consultar

Blazor obtiene el listado mediante:

```http
GET /api/clientes
```

La información recibida desde la API se muestra en la interfaz del sistema.

---

## 🩷 Actualizar

Cuando el usuario modifica la información de un cliente, Blazor realiza:

```http
PUT /api/clientes/{id}
```

Los nuevos datos son enviados en formato JSON hacia la API.

---

## 🌷 Eliminar

Para eliminar un cliente se utiliza:

```http
DELETE /api/clientes/{id}
```

Después de completar la operación, Blazor actualiza el listado de clientes.

---

# 💗 Separación de responsabilidades

El proyecto mantiene separadas las responsabilidades de cada componente:

```text
🌸 Blazor WebAssembly
        ↓
   Interfaz de usuario

💗 API REST
        ↓
   Lógica y procesamiento

🌷 Entity Framework Core
        ↓
   Acceso a los datos

🩷 MySQL
        ↓
   Persistencia
```

> 💡 **Blazor WebAssembly no se conecta directamente a MySQL.**

Toda operación relacionada con los clientes debe realizarse mediante la **API REST**.

---

# 🌸 Requisitos

Para ejecutar el proyecto se recomienda contar con:

- 💗 **.NET SDK 10**
- 🌷 **Visual Studio Code o Visual Studio 2022**
- 🩷 **Git**
- 🌐 **Navegador web moderno**
- ⚙️ **Programacion2ClientesAPI en ejecución**

---

# 🌷 Autora

### 💗 Sharon Georgette Nahomy Calancho Toledo

**Curso:** Programación II  
**Proyecto:** Sistema de Gestión de Clientes  
**Frontend:** Blazor WebAssembly  
**Backend:** ASP.NET Core Web API  
**Base de datos:** MySQL

---

### 🌸 Tecnologías principales

`C#` · `.NET 10` · `Blazor WebAssembly` · `ASP.NET Core` · `REST API` · `MySQL` · `Bootstrap`

---

> 🌷 **Proyecto desarrollado con fines académicos para el curso de Programación II.**
