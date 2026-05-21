# Guía de Entregables Técnicos: Especificación, Pruebas y Documentación

Esta guía práctica explica qué contiene cada uno de los tres archivos de entregables del proyecto de Gestión Documental, qué se visualiza en ellos y cómo utilizarlos paso a paso.

---

## Resumen de los 3 Archivos

| Archivo | Formato | Propósito | ¿Qué se ve? | ¿Cómo se utiliza? |
| :--- | :--- | :--- | :--- | :--- |
| **`openapi.yaml`** | YAML | Contrato Técnico y Especificación | Estructura formal de endpoints, parámetros, respuestas y seguridad (Swagger). | Importándolo en **Swagger Editor**, Swagger UI o en generadores de código de integración. |
| **`postman_collection.json`** | JSON | Suite de Pruebas Ejecutables | Peticiones HTTP reales configuradas con variables de entorno y Feature Flags (Mocks). | Importándolo en **Postman** para ejecutar pruebas en vivo contra los endpoints de AWS. |
| **`api_documentation.md`** | Markdown | Documentación de Arquitectura y Flujos | Diagramas de secuencia de negocio, detalle del flujo OAuth 2.0 y Cognito, reglas de mensajería. | Abriéndolo en un **lector Markdown** (VS Code, GitHub, etc.) como manual de integración. |

---

## 1. Archivo `openapi.yaml` (Especificación OpenAPI 3.0 / Swagger)

### ¿Qué se ve en este archivo?
Es una especificación estandarizada y autodescriptiva que define la firma técnica de tu API. Al renderizarse visualmente, muestra:
- **Endpoints y Rutas**: Todos los paths HTTP disponibles (`POST /upload`, `GET /documents`, etc.).
- **Esquema de Datos (Schemas)**: Las estructuras exactas de JSON requeridas para enviar información y devueltas en la respuesta (el wrapper `{ success, code, data }`).
- **Seguridad**: La configuración para el encabezado `Authorization: Bearer <TOKEN>` y la integración con el flujo de Cognito.
- **Feature Flags**: Documentación de la cabecera `x-mock-data` para recibir respuestas simuladas.

### ¿Cómo utilizarlo?
1. **Visualización Interactiva**:
   - Abre tu navegador e ingresa a [Swagger Editor](https://editor.swagger.io/).
   - Copia el contenido del archivo `openapi.yaml` y pégalo en el panel izquierdo.
   - Navega e inspecciona la API en el panel derecho de forma interactiva.
2. **Generar Clientes de API**:
   - Puedes usar herramientas como [OpenAPI Generator](https://openapi-generator.tech/) para introducir este archivo y crear automáticamente librerías cliente en TypeScript para Angular, en Java, Python, etc.

---

## 2. Archivo `postman_collection.json` (Colección de Postman)

### ¿Qué se ve en este archivo?
Es una suite de pruebas lista para ejecutarse. Al importarla, verás una colección llamada **"Document Management System API"** estructurada de la siguiente forma:
- **Carpeta Auth**: Contiene la petición para obtener el JWT Token de Cognito enviando las credenciales de cliente.
- **Carpeta Documents**: Peticiones para todo el ciclo de vida del documento.
- **Carpeta Stats**: Petición para estadísticas del dashboard.
- **Variables**: Pestaña de configuración con variables de entorno (`api_url`, `client_id`, `client_secret`, etc.).

### ¿Cómo utilizarlo?
1. Abre **Postman**.
2. Haz clic en **Import** (esquina superior izquierda) y selecciona el archivo `postman_collection.json`.
3. Configura las credenciales de Cognito en las variables de la colección si deseas probar producción real.
4. **Para Mocks (Sin dependencias)**:
   - Activa el header `x-mock-data` con valor `true` en la pestaña **Headers** de cualquier petición.
   - Haz clic en **Send** y verás la respuesta de simulación estructurada inmediatamente.

---

## 3. Archivo `api_documentation.md` (Manual y Flujos de Arquitectura)

### ¿Qué se ve en este archivo?
Es el manual técnico y conceptual del proyecto, escrito en Markdown. Muestra:
- **Estándar JSON**: Explicación detallada del porqué de la envoltura en `"data"` y las propiedades `success` y `code`.
- **Diagramas de Flujo (Mermaid)**: Diagramas interactivos que representan visualmente:
  1. El flujo de carga asíncrona de archivos grandes mediante URLs pre-firmadas hacia S3.
  2. El flujo de descarga segura con validación de propiedad de archivos.
- **Guía de Cognito**: Instrucciones de cómo solicitar el token mediante cURL o solicitudes HTTP tradicionales.

### ¿Cómo utilizarlo?
- **Lectura en VS Code**: Abre el archivo en VS Code y presiona `Ctrl + Shift + V` para abrir la vista previa formateada y ver los diagramas.
- **Lectura en GitHub**: Súbelo al repositorio y GitHub renderizará automáticamente las tablas, textos y los diagramas de secuencia interactivos de Mermaid.
