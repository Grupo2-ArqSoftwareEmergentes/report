# Capítulo V: Tactical-Level Software Design.
## 5.1.Bounded Context: Identity & Access Management
El Bounded Context de Identidad y Acceso agrupa las funcionalidades vinculadas a la autenticación, autorización y gestión del acceso dentro de la plataforma. Su propósito es garantizar una correcta identificación de cada usuario, una administración segura de sus sesiones y un control de permisos que regule el acceso a las distintas funciones del sistema conforme al rol asignado a cada usuario.
### 5.1.1. Domain Layer.
La capa de dominio del Bounded Context Identity & Access (IAM) en VineVault concentra las reglas de negocio relacionadas con la identidad de los usuarios, la autenticación, la autorización y la gestión del ciclo de vida de las sesiones. Su propósito es mantener la coherencia del modelo mediante conceptos propios del dominio, evitando dependencias con tecnologías específicas como bases de datos, frameworks o servicios externos.

Dentro de VineVault, este contexto es fundamental ya que define quién puede acceder al sistema, bajo qué condiciones puede hacerlo y qué funcionalidades puede utilizar una vez autenticado. Esto resulta especialmente relevante considerando que la plataforma diferencia claramente entre perfiles de usuario con distintos niveles de acceso.


| Elemento          | Descripción                                                                                                                                                          |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User**          | Representa al usuario registrado en VineVault. Contiene su identidad, estado de cuenta, proveedor de autenticación y roles asignados.                                |
| **Role**          | Define el tipo de usuario dentro del sistema (Home User o Facility Admin), determinando su alcance funcional.                                                        |
| **Permission**    | Representa las acciones autorizadas dentro de la plataforma, utilizadas para controlar el acceso a funcionalidades como inventario, analítica o gestión de usuarios. |
| **Session**       | Representa una sesión autenticada activa, asociada a un usuario y con un tiempo de validez definido.                                                                 |
| **Refresh Token** | Credencial utilizada para renovar sesiones sin requerir reautenticación, bajo políticas de seguridad como rotación de tokens.                                        |
| **Auth Provider** | Define el origen de autenticación del usuario, pudiendo ser local (email/password) o federado (por ejemplo, Google OAuth2).                                          |

Las reglas de negocio más relevantes de este contexto en VineVault son las siguientes:

| Regla de negocio             | Descripción                                                                                                                                                        |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Unicidad de identidad**    | No puede existir más de una cuenta activa asociada al mismo correo electrónico dentro de la plataforma.                                                            |
| **Verificación previa**      | Las cuentas registradas mediante email y password deben verificar su correo antes de acceder a funcionalidades como gestión de inventario, telemetría o analítica. |
| **Roles obligatorios**       | Todo usuario autenticado debe poseer al menos un rol válido (Home User o Facility Admin), el cual define su alcance sobre los módulos del sistema.                 |
| **Sesión válida**            | Ninguna operación protegida (ej. registrar botellas, consultar analítica, recibir alertas) puede ejecutarse sin una sesión activa o un token de acceso válido.     |
| **Rotación de credenciales** | Cada uso válido del refresh token invalida el anterior y genera uno nuevo, reduciendo el riesgo de reutilización indebida.                                         |
| **Revocación inmediata**     | La desactivación de la cuenta o el cierre de sesión debe invalidar todas las sesiones activas asociadas al usuario.                                                |

Estas reglas garantizan la integridad del modelo de identidad y acceso, alineando el comportamiento del sistema con los requerimientos funcionales del IAM (registro, autenticación, autorización y gestión de sesiones), así como con los requerimientos no funcionales de seguridad, tales como control de acceso, expiración de sesiones y protección frente a uso indebido de credenciales.

### 5.1.2. Interface Layer.

La capa de interfaz del Bounded Context Identity & Access (IAM) en VineVault expone las capacidades del dominio hacia los distintos clientes del sistema, principalmente la aplicación móvil (canal principal), el panel web (analítica avanzada) y la landing page. Su responsabilidad es recibir solicitudes, validarlas, transformarlas en comandos o consultas y delegar su ejecución a la capa de aplicación, manteniendo desacoplada la lógica de presentación de las reglas de negocio.

En esta capa se ubican los controladores HTTP, los objetos de transferencia de datos (DTOs), los mecanismos de validación de entrada y los filtros de seguridad necesarios para proteger los recursos del sistema. Desde la perspectiva del usuario, esta capa representa la puerta de entrada a procesos como registro, autenticación, verificación de cuenta, renovación de sesión y cierre de sesión.

Endpoints Principales

| Endpoint u operación             | Tipo de acceso     | Propósito                                                          |
| -------------------------------- | ------------------ | ------------------------------------------------------------------ |
| **POST /auth/register**          | Público            | Registrar un nuevo usuario mediante email y password.              |
| **POST /auth/login**             | Público            | Autenticar al usuario y emitir credenciales de acceso.             |
| **POST /auth/verify-email**      | Público            | Confirmar la identidad del usuario mediante token de verificación. |
| **POST /auth/refresh**           | Público controlado | Renovar la sesión usando un refresh token válido.                  |
| **POST /auth/logout**            | Protegido          | Revocar la sesión actual del usuario.                              |
| **POST /auth/oauth/google**      | Público            | Autenticación federada mediante Google.                            |
| **GET /auth/me**                 | Protegido          | Obtener información del usuario autenticado.                       |
| **PATCH /users/{id}/deactivate** | Protegido          | Desactivar una cuenta y revocar sus sesiones.                      |

### 5.1.3. Application Layer.
La capa de aplicación del Bounded Context Identity & Access (IAM) en VineVault se encarga de orquestar los casos de uso que materializan los procesos de autenticación y autorización definidos por el negocio. A diferencia de la capa de dominio, esta capa no contiene reglas fundamentales, sino que coordina la interacción entre entidades, repositorios, políticas de seguridad, servicios externos y eventos necesarios para ejecutar cada flujo de manera consistente.

Su propósito es traducir las acciones del usuario (provenientes de la app móvil o el panel web) en operaciones concretas sobre el dominio, garantizando que se respeten las reglas de seguridad y acceso a los distintos módulos del sistema, como inventario, telemetría y analítica.

| Caso de uso                | Descripción                                                                                                        |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **RegisterUser**           | Registra un nuevo usuario, valida la unicidad del correo y activa el flujo de verificación.                        |
| **VerifyEmail**            | Confirma la cuenta del usuario y habilita el acceso a funcionalidades como gestión de cava y consulta de sensores. |
| **LoginUser**              | Valida credenciales o identidad federada, crea una sesión y emite tokens de acceso.                                |
| **RefreshSession**         | Renueva la sesión autenticada mediante rotación segura de refresh tokens.                                          |
| **LogoutUser**             | Revoca la sesión actual y evita el reuso de credenciales invalidadas.                                              |
| **DeactivateAccount**      | Desactiva la cuenta del usuario y revoca todas sus sesiones activas.                                               |
| **AssignRoleToUser**       | Asigna o modifica el rol del usuario (Home User o Facility Admin).                                                 |
| **AuthenticateWithGoogle** | Procesa la autenticación federada y la adapta al modelo interno de VineVault.                                      |

### 5.1.4. Infrastructure Layer.
La capa de infraestructura del Bounded Context Identity & Access (IAM) en VineVault implementa los mecanismos técnicos que permiten materializar las necesidades del dominio y de la capa de aplicación en el entorno real de ejecución. En esta capa se concretan aspectos como la persistencia de datos, la autenticación, la gestión de tokens y la integración con proveedores externos de identidad.

Las decisiones tecnológicas adoptadas priorizan bajo costo, simplicidad operativa y facilidad de mantenimiento, manteniendo al mismo tiempo un nivel adecuado de seguridad, escalabilidad y desacoplamiento arquitectónico.

| Recurso                       | Responsabilidad                                                                         |
| ----------------------------- | --------------------------------------------------------------------------------------- |
| **PostgreSQL**                | Persistir usuarios, roles, permisos y relaciones de autorización de forma estructurada. |
| **JWT Provider (stateless)**  | Generar y validar access tokens para autenticación en endpoints protegidos.             |
| **Password Encoder (bcrypt)** | Hashear y verificar contraseñas de forma segura.                                        |
| **Google OAuth2**  | Permitir autenticación federada sin gestionar credenciales directamente.                |


### 5.1.6. Bounded Context Software Architecture Component Level Diagrams.
### 5.1.7. Bounded Context Software Architecture Code Level Diagrams.
#### 5.1.7.1.Bounded Context Domain Layer Class Diagrams.
#### 5.1.7.2.Bounded Context Database Design Diagram.

## 5.X.Bounded Context: <Bounded Context Name>
### 5.X.1. Domain Layer.
### 5.X.2. Interface Layer.
### 5.X.3. Application Layer.
### 5.X.4. Infrastructure Layer.
### 5.X.6. Bounded Context Software Architecture Component Level Diagrams.
### 5.X.7. Bounded Context Software Architecture Code Level Diagrams.
#### 5.X.7.1.Bounded Context Domain Layer Class Diagrams.
#### 5.X.7.2.Bounded Context Database Design Diagram.