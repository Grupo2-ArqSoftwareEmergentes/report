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

**Reglas de negocio**

Las reglas principales de la capa de dominio son las siguientes:

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

Su propósito es traducir las acciones del usuario en operaciones concretas sobre el dominio, garantizando que se respeten las reglas de seguridad y acceso a los distintos módulos del sistema, como inventario, telemetría y analítica.

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

## 5.2.Bounded Context: Billing
El Bounded Context Billing agrupa la lógica de negocio vinculada a planes, suscripciones, checkout, pagos e invoices dentro de VineVault. Su responsabilidad es gobernar el acceso a las capacidades del sistema según el tipo de usuario, permitiendo diferenciar entre funcionalidades básicas de gestión de cava y capacidades avanzadas como analítica histórica, multiusuario y monitoreo extendido.

### 5.2.1. Domain Layer.
La capa de dominio del Bounded Context Billing en VineVault concentra las reglas de negocio relacionadas con planes, suscripciones, cobros, facturación y control de acceso a funcionalidades avanzadas del sistema. Su objetivo es representar de manera explícita cómo se gestiona el acceso a capacidades como analítica, monitoreo histórico y gestión multiusuario, así como las condiciones bajo las cuales un usuario adquiere, mantiene o pierde dichos beneficios.

Este contexto tiene un rol estratégico dentro del sistema, ya que conecta directamente la propuesta de valor de VineVault con su sostenibilidad operativa. A diferencia de enfoques tradicionales que limitan el uso en función del volumen de inventario, VineVault implementa un modelo de monetización por valor añadido, donde las restricciones y beneficios están definidos por el nivel de inteligencia y control que el sistema proporciona al usuario.

En este sentido, el dominio de Billing no controla cuánto puede almacenar un usuario, sino qué tan avanzadas son las capacidades a las que puede acceder.

| Elemento del dominio | Descripción                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| Subscription         | Representa la relación activa o inactiva entre un usuario (o negocio) y un plan.                   |
| Plan                 | Define las capacidades habilitadas, como acceso a analítica, historial de sensores o multiusuario. |
| Checkout Session     | Representa el proceso temporal de pago antes de su confirmación.                                   |
| Invoice              | Representa la evidencia de una transacción económica o ciclo de facturación.                       |
| Payment Outcome      | Representa el resultado del intento de cobro (exitoso o fallido).                                  |
| Trial Period         | Representa el periodo inicial con acceso a funcionalidades avanzadas por tiempo limitado.          |

El agregado central de este bounded context es Subscription, ya que desde esta raíz se gobiernan decisiones como el plan contratado, su estado actual, la duración del trial, la renovación, la cancelación y el impacto funcional de estos cambios sobre el resto del sistema.

Como soporte semántico, el modelo incorpora objetos de valor como PlanId, SubscriptionStatus, BillingPeriod, Money, InvoiceId y CheckoutSessionId, los cuales permiten expresar conceptos del negocio con consistencia y precisión.

**Modelo de planes basado en capacidades**
| Plan               | Capacidades                                                                                                                 |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| Home (Freemium)    | Gestión de inventario ilimitado, monitoreo en tiempo real, historial limitado de sensores, sin analítica avanzada           |
| Business (Premium) | Inventario ilimitado, historial completo, analítica avanzada, reportes de rotación, sugerencias inteligentes y multiusuario |

Este diseño refleja que el sistema no impone límites sobre la cantidad de botellas, sino sobre el nivel de inteligencia y control disponible para el usuario.

**Reglas de negocio**

Las reglas principales de la capa de dominio son las siguientes:

| Regla de negocio             | Descripción                                                                                                                      |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Monetización por capacidades | El acceso a funcionalidades se define por el nivel de análisis y control habilitado, no por la cantidad de botellas registradas. |
| Trial inicial                | Todo usuario nuevo puede acceder a un periodo de prueba con capacidades Business por tiempo limitado.                            |
| Downgrade automático         | Al finalizar el trial sin activación de pago, el usuario regresa al plan Home con restricciones en analítica e historial.        |
| Activación por pago válido   | Una suscripción Business solo se activa cuando el pago ha sido confirmado.                                                       |
| Persistencia del estado      | Todo cambio en la suscripción debe mantenerse de forma consistente y auditable.                                                  |
| Restricción de capacidades   | Funcionalidades avanzadas como analítica histórica, reportes y multiusuario solo están disponibles con suscripción activa.       |
| Ventana de datos             | Usuarios Freemium acceden únicamente a un historial limitado de datos de sensores.                                               |
| Cancelación controlada       | La cancelación implica la pérdida de capacidades avanzadas, manteniendo acceso básico al inventario.                             |
| Inventario sin restricciones | No existe límite en la cantidad de botellas para ningún plan.                                                                    |

### 5.2.2. Interface Layer.
La capa de interfaz del Bounded Context Billing en VineVault expone al exterior los procesos vinculados a suscripciones, consulta de planes, gestión de capacidades habilitadas, checkout, facturación y control del ciclo comercial del usuario. Su responsabilidad es recibir solicitudes provenientes de la Mobile App y del Panel Web, validarlas y delegarlas a la capa de aplicación mediante contratos claros y consistentes.

Desde la experiencia de usuario, esta capa representa el punto de contacto con las operaciones comerciales del sistema. A través de ella, el usuario puede comprender qué capacidades están disponibles en cada plan, activar un periodo de prueba, contratar el plan Business, consultar el estado de su suscripción y verificar si tiene acceso a funcionalidades avanzadas como analítica histórica o monitoreo extendido.

| Endpoint u operación               | Tipo de acceso     | Propósito                                                                                         |
| ---------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------- |
| GET /billing/plans                 | Público            | Consultar el catálogo de planes y las capacidades asociadas (analítica, historial, multiusuario). |
| GET /billing/subscription          | Protegido          | Recuperar el estado actual de la suscripción y capacidades habilitadas del usuario.               |
| POST /billing/trial/start          | Protegido          | Iniciar el periodo de prueba con acceso a funcionalidades Business.                               |
| POST /billing/checkout-session     | Protegido          | Crear una sesión de pago para activar o cambiar a plan Business.                                  |
| POST /billing/webhooks/stripe      | Externo controlado | Recibir eventos del proveedor de pagos (confirmación, renovación, fallo, cancelación).            |
| PATCH /billing/subscription/cancel | Protegido          | Solicitar la cancelación de la suscripción activa.                                                |
| GET /billing/invoices              | Protegido          | Consultar el historial de facturación del usuario o negocio.                                      |

### 5.2.3. Application Layer.
La capa de aplicación del Bounded Context Billing en VineVault orquesta los casos de uso relacionados con el ciclo comercial del usuario, desde el inicio del periodo de prueba hasta la activación, renovación, cambio o cancelación de la suscripción. Su propósito es coordinar las entidades del dominio, repositorios, integraciones externas y la publicación de eventos, garantizando que cada transición comercial se ejecute de forma consistente y alineada con el modelo de monetización basado en capacidades.

A diferencia de sistemas tradicionales, esta capa no gestiona restricciones por volumen, sino que controla la habilitación o restricción de funcionalidades como analítica histórica, monitoreo extendido y gestión multiusuario.

| Caso de uso             | Descripción                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| StartTrialSubscription  | Inicia el periodo de prueba habilitando temporalmente capacidades Business para usuarios elegibles. |
| CreateCheckoutSession   | Genera una sesión de pago con el proveedor externo para contratar o actualizar el plan.             |
| ConfirmPaymentOutcome   | Procesa el resultado del pago y determina si se debe activar o rechazar la suscripción.   |
| ActivateSubscription    | Activa la suscripción Business y habilita capacidades avanzadas del sistema.                        |
| ChangePlan              | Gestiona el cambio entre planes ajustando dinámicamente las capacidades disponibles.                |
| CancelSubscription      | Cancela la suscripción y restringe el acceso a funcionalidades avanzadas.                           |
| ExpireTrialAndDowngrade | Detecta la expiración del trial y aplica downgrade automático al plan Home.                         |
| GetSubscriptionStatus   | Expone el estado comercial actual y las capacidades habilitadas del usuario.                        |

### 5.2.4. Infrastructure Layer.
La capa de infraestructura del Bounded Context Billing en VineVault implementa los componentes técnicos necesarios para soportar la persistencia de planes y suscripciones, la integración con el proveedor de pagos, el registro de facturación y el procesamiento seguro de eventos externos asociados al cobro. Esta capa traduce las necesidades del dominio comercial en mecanismos concretos de almacenamiento, comunicación e interoperabilidad.

En el contexto de VineVault, Billing se apoya principalmente en PostgreSQL para la persistencia de información comercial, y en un proveedor externo de pagos (como Stripe) para la gestión de checkout, confirmación de pagos y notificación de eventos. Asimismo, esta capa se integra con componentes compartidos del sistema para logging, auditoría, configuración segura y gestión de credenciales.

| Recurso de infraestructura        | Responsabilidad                                                                                |
| --------------------------------- | ---------------------------------------------------------------------------------------------- |
| PostgreSQL                        | Persistir planes, suscripciones, historial de facturación y relación con usuarios o negocios.  |
| Payment Provider API  | Crear sesiones de pago, gestionar renovaciones y notificar resultados de transacciones.        |
| Webhook Handler                   | Recibir, validar y procesar eventos externos de pago (confirmaciones, fallos, cancelaciones).  |
| Billing Repository Adapter        | Implementar el acceso persistente a entidades como Subscription, Plan e Invoice.               |
| Audit and Logging Components      | Registrar cambios de estado comercial, errores de pago y eventos relevantes para trazabilidad. |
| Secure Configuration Manager      | Gestionar credenciales, claves API y configuraciones sensibles del proveedor de pagos.         |

### 5.2.6. Bounded Context Software Architecture Component Level Diagrams.
### 5.2.7. Bounded Context Software Architecture Code Level Diagrams.
#### 5.2.7.1.Bounded Context Domain Layer Class Diagrams.
#### 5.2.7.2.Bounded Context Database Design Diagram.

## 5.3.Bounded Context: Notification
El Bounded Context Notification centraliza la gestión del envío de comunicaciones hacia los usuarios de VineVault, incluyendo alertas críticas, mensajes informativos y notificaciones derivadas de eventos del sistema. Su finalidad es proporcionar una capacidad transversal de comunicación que permita a otros bounded contexts informar situaciones relevantes, como anomalías ambientales, recordatorios de consumo o actualizaciones del sistema, manteniendo consistencia, trazabilidad y control sobre cada envío.

### 5.3.1. Domain Layer.
La capa de dominio del Bounded Context Notification modela la gestión de mensajes, solicitudes de envío, canales de comunicación y trazabilidad de las notificaciones emitidas por VineVault. Su responsabilidad es asegurar que los eventos generados por otros bounded contexts, como Environmental Monitoring o Inventory Intelligence, puedan traducirse en comunicaciones efectivas, consistentes y alineadas con las preferencias del usuario.

Este contexto no decide cuándo ocurre una anomalía térmica o cuándo debe generarse una recomendación de consumo; su función es encargarse del ciclo de vida de la notificación resultante. Por ello, constituye una capacidad transversal de soporte para otro BC.

| **Elemento del dominio**     | **Descripción**                                                                                             |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Notification Message         | Representa el contenido de la notificación generada, incluyendo título, cuerpo y metadata contextual.       |
| Delivery Request             | Representa una solicitud concreta de envío dirigida a uno o varios usuarios.                                |
| Delivery Channel             | Representa el medio de comunicación utilizado, como notificaciones push o correo electrónico.               |
| Notification History         | Representa el registro trazable de notificaciones enviadas, pendientes o fallidas.                          |
| User Notification Preference | Representa la configuración del usuario respecto a los canales habilitados y la frecuencia de notificación. |


**Reglas de negocio**

Las reglas de dominio incluyen respetar las preferencias de notificación del usuario, garantizar que los mensajes críticos tengan prioridad, registrar el resultado de cada intento de entrega y permitir reintentos en caso de fallos. Asimismo, el sistema debe soportar tanto notificaciones en tiempo real como comunicaciones informativas derivadas de análisis periódicos.

### 5.3.2. Interface Layer.
La capa de interfaz del Bounded Context Notification expone operaciones relacionadas con la consulta del historial de notificaciones, la gestión de preferencias del usuario y la recepción de solicitudes internas de envío provenientes de otros bounded contexts de VineVault. Asimismo, actúa como el punto de entrada que permite traducir eventos del sistema, como anomalías ambientales o recomendaciones de consumo, en solicitudes formales de notificación.

| **Endpoint u operación**         | **Tipo de acceso** | **Propósito**                                                                                              |
| -------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| GET /notifications/history       | Protegido          | Consultar el historial de notificaciones enviadas al usuario, incluyendo estado y tipo de mensaje.         |
| PATCH /notifications/preferences | Protegido          | Configurar canales habilitados (push, email) y preferencias de recepción del usuario.                      |
| GET /notifications/settings      | Protegido          | Obtener la configuración actual de notificaciones del usuario.                                             |
| POST /notifications/send         | Interno controlado | Registrar una solicitud de envío generada por otros bounded contexts (ej. alerta térmica o recomendación). |
| POST /notifications/test         | Protegido          | Permitir al usuario validar la configuración mediante el envío de una notificación de prueba.              |

La interfaz se apoya en contratos como NotificationHistoryResponse, NotificationPreferenceRequest, NotificationSettingsResponse y DeliveryRequestDto. Estos contratos definen la estructura de los datos intercambiados entre clientes, otros bounded contexts y el sistema de notificaciones.

Las validaciones de esta capa se enfocan en verificar la identidad del usuario autenticado, la consistencia de los canales seleccionados, la existencia de destinatarios válidos y la integridad de los datos necesarios para construir el mensaje. En el caso de solicitudes internas, se asegura además que provengan de bounded contexts autorizados como Environmental Monitoring BC o Inventory Intelligence BC.

De este modo, la Interface Layer de Notification habilita una comunicación estructurada entre los eventos del sistema y la capacidad especializada de envío de mensajes, permitiendo que VineVault entregue información crítica de manera confiable y controlada.

### 5.3.3. Application Layer.
La capa de aplicación del Bounded Context Notification coordina la transformación de eventos del sistema en notificaciones concretas dirigidas a los usuarios. Su responsabilidad es orquestar la selección del contenido, la resolución de destinatarios, la evaluación de preferencias y el despacho de mensajes a través de los canales disponibles, garantizando trazabilidad en todo el proceso.

En el contexto de VineVault, esta capa permite convertir eventos como anomalías de temperatura, pérdida de conexión con sensores o recomendaciones de consumo en comunicaciones efectivas hacia el usuario final.

| **Caso de uso**              | **Descripción**                                                                                                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| RequestNotificationDelivery  | Registrar una solicitud de envío proveniente de otros bounded contexts, como Environmental Monitoring o Inventory Intelligence.            |
| ResolveRecipients            | Determinar los destinatarios efectivos en función del usuario asociado a la cava y sus preferencias configuradas.                          |
| EvaluateNotificationPriority | Clasificar la notificación según su criticidad (por ejemplo, alertas críticas vs. mensajes informativos).                                  |
| RenderNotificationMessage    | Construir el contenido final del mensaje utilizando datos de contexto (ej. temperatura actual, nombre de la cava, recomendación generada). |
| DispatchNotification         | Enviar la notificación a través del canal correspondiente, como push móvil o correo electrónico.                                           |
| RecordDeliveryOutcome        | Registrar el resultado de la entrega, incluyendo éxito, fallo o reintento.                                                                 |

Estos casos de uso pueden implementarse mediante servicios como NotificationAppService, NotificationRoutingService, MessageRenderingService y NotificationHistoryService. La coordinación entre estos servicios permite desacoplar la intención de comunicar (generada por otros bounded contexts) de la lógica concreta de construcción y envío del mensaje.

Adicionalmente, esta capa puede integrar mecanismos de priorización y manejo de eventos en tiempo real, asegurando que notificaciones críticas (como una temperatura fuera de rango que pueda dañar el vino) sean procesadas y enviadas con mayor urgencia que comunicaciones informativas.

De este modo, la Application Layer de Notification actúa como el orquestador que transforma solicitudes abstractas de comunicación en notificaciones concretas, asegurando que cada mensaje enviado por VineVault tenga el contenido, canal y nivel de prioridad adecuados según el contexto de negocio.

### 5.3.4. Infrastructure Layer.
La capa de infraestructura del Bounded Context Notification implementa los mecanismos técnicos necesarios para la persistencia del historial de notificaciones, la gestión de solicitudes de envío y la integración con proveedores externos de mensajería. En el contexto de VineVault, esta capa permite materializar el envío de alertas críticas —como anomalías de temperatura o fallos de conexión con sensores— mediante canales como notificaciones push y correo electrónico.

Siguiendo la arquitectura del sistema, este contexto se apoya en PostgreSQL para la trazabilidad de notificaciones y en servicios externos como Firebase Cloud Messaging (FCM) para notificaciones push y proveedores SMTP o APIs de email transaccional para el envío de correos.

| **Recurso de infraestructura**    | **Responsabilidad**                                                                     |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| PostgreSQL                        | Persistir solicitudes de envío, historial de notificaciones y preferencias del usuario. |
| Firebase Cloud Messaging (FCM)    | Gestionar el envío de notificaciones push en tiempo real hacia dispositivos móviles.    |
| Email Service Provider (SMTP/API) | Ejecutar el envío de correos electrónicos para alertas o comunicaciones informativas.   |
| Delivery Repository Adapter       | Registrar resultados de envío, estados de notificación y reintentos.                    |
| Notification Channel Adapter      | Abstraer la integración con distintos canales (push, email).                            |

Las estructuras principales de persistencia pueden incluir notification_requests, notification_history y user_notification_preferences, permitiendo mantener un registro completo de cada comunicación emitida por el sistema.

Adicionalmente, la infraestructura debe soportar mecanismos de reintentos automáticos ante fallos de entrega, registro de logs para diagnóstico y capacidades de observabilidad que permitan monitorear métricas como tasa de éxito, latencia de envío y frecuencia de alertas críticas. Esto resulta especialmente importante en VineVault, donde una notificación tardía o fallida puede comprometer la conservación de la cava.

En consecuencia, la Infrastructure Layer de Notification hace operativa la capacidad comunicacional de VineVault, conectando las decisiones del negocio con servicios reales de mensajería y garantizando la trazabilidad completa de cada notificación enviada.

### 5.3.6. Bounded Context Software Architecture Component Level Diagrams.
### 5.3.7. Bounded Context Software Architecture Code Level Diagrams.
#### 5.3.7.1.Bounded Context Domain Layer Class Diagrams.
#### 5.3.7.2.Bounded Context Database Design Diagram.


## 5.X.Bounded Context: <Bounded Context Name>
### 5.X.1. Domain Layer.
### 5.X.2. Interface Layer.
### 5.X.3. Application Layer.
### 5.X.4. Infrastructure Layer.
### 5.X.6. Bounded Context Software Architecture Component Level Diagrams.
### 5.X.7. Bounded Context Software Architecture Code Level Diagrams.
#### 5.X.7.1.Bounded Context Domain Layer Class Diagrams.
#### 5.X.7.2.Bounded Context Database Design Diagram.