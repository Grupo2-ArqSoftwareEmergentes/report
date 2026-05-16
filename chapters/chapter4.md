# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Attribute-Driven Design.
En esta sección se evidencia el proceso de Attribute-Driven Design para la solución. 

### 4.1.1. Design Purpose.
La razón fundamental detrás del diseño de VineVault es garantizar una gestión eficiente, segura y simplificada de cavas y bodegas, respondiendo a las necesidades reales de coleccionistas, aficionados y establecimientos que manejan bebidas premium. El propósito central es reducir la incertidumbre en el control del inventario y prevenir la pérdida de productos causada por condiciones ambientales inadecuadas, mediante una solución tecnológica que integra monitoreo en tiempo real, alertas inteligentes y digitalización del inventario.
- **Facilitar una Experiencia de Usuario Simple e Intuitiva:**
  La plataforma está diseñada para minimizar la carga operativa del usuario, evitando procesos manuales complejos. A través de funcionalidades como escaneo de botellas, registro automatizado y visualización clara del inventario, los usuarios pueden gestionar su colección de forma rápida y sin esfuerzo.

- **Optimizar el Control y la Protección de la Colección:**
  El sistema permite a los usuarios mantener visibilidad constante sobre sus botellas, así como monitorear variables críticas como temperatura y humedad. Esto reduce significativamente el riesgo de deterioro del producto y mejora la toma de decisiones sobre consumo o conservación.

- **Atender Necesidades Específicas de Cada Segmento:**
  - **Coleccionistas y Aficionados:** requieren organización sencilla, acceso rápido a su inventario y recomendaciones sobre el momento óptimo de consumo.
  - **Restaurantes y Negocios:** necesitan control preciso del stock, reducción de pérdidas y monitoreo continuo para asegurar la calidad del producto ofrecido.

- **Asegurar Monitoreo Confiable y Respuesta en Tiempo Real:**
  - Actualización de condiciones ambientales en tiempo real.
  - Envío de alertas inmediatas ante variaciones críticas.
  - Disponibilidad constante de la plataforma para consulta remota.
  - Escalabilidad para gestionar múltiples cavas o colecciones simultáneamente.


### 4.1.2. Attribute-Driven Design Inputs.
 #### 4.1.2.1. Primary Functionality (Primary User Stories).

En esta sección se especifican las User Stories primarias que resultan críticas para la arquitectura y el funcionamiento general de VineVault. Estas funcionalidades constituyen la base del sistema, ya que permiten cubrir los procesos centrales de registro de inventario, monitoreo ambiental y protección de las colecciones de vinos y destilados.

- **Registro de botellas (US04, US05):**
  Esta funcionalidad es fundamental para la digitalización de la cava. Permite ingresar botellas de forma manual o mediante escaneo, lo que obliga a la arquitectura a soportar almacenamiento estructurado de datos, procesamiento de imágenes y consultas a bases de datos externas. Impacta directamente en el modelo de datos y en la experiencia de usuario al reducir la fricción en el registro.

- **Gestión y actualización de inventario (US06, US07):**
  El sistema permite mantener actualizado el stock mediante acciones como descorchar botellas y realizar búsquedas avanzadas. Esta funcionalidad es clave para la trazabilidad del inventario, requiriendo sincronización inmediata de datos y consultas eficientes que permitan al usuario acceder rápidamente a la información.

- **Vinculación y gestión de sensores IoT (US08, US11):**
  La integración con sensores es esencial para el monitoreo ambiental. Esta funcionalidad requiere que la arquitectura soporte comunicación con dispositivos externos, manejo de múltiples sensores y configuración dinámica, impactando en la capa de integración IoT y en la escalabilidad del sistema.

- **Monitoreo ambiental en tiempo real (US09):**
  Permite visualizar variables críticas como temperatura de forma continua. Esto exige una arquitectura capaz de procesar datos en tiempo real, actualizar dashboards periódicamente y mantener consistencia entre dispositivos, lo cual impacta en el diseño de flujos de datos y almacenamiento temporal.

- **Alertas térmicas inteligentes (US10):**
  El sistema notifica al usuario ante condiciones que pueden dañar el producto. Esta funcionalidad implica una arquitectura orientada a eventos, con detección de umbrales, generación de alertas y envío de notificaciones en tiempo real, garantizando tiempos de respuesta bajos y alta confiabilidad.

- **Análisis histórico y reportes (US12, US13):**
  Permite evaluar el comportamiento ambiental y la salud de la cava a lo largo del tiempo. Esta funcionalidad requiere almacenamiento histórico de datos, generación de gráficos interactivos y procesamiento de información agregada, impactando en la capa analítica del sistema.

- **Predicción de madurez y recomendaciones (US14):**
  Esta funcionalidad agrega valor al usuario al indicar el momento óptimo de consumo de las botellas. Implica el uso de lógica de negocio basada en reglas o modelos predictivos, afectando la arquitectura en términos de procesamiento de datos y generación de insights personalizados.

#### 4.1.2.2. Quality attribute Scenarios.

En esta sección se detallan los escenarios iniciales de atributos de calidad que influyen directamente en la arquitectura de VineVault. Estos escenarios permiten definir requisitos no funcionales clave relacionados con el monitoreo en tiempo real, la confiabilidad del sistema y la protección de datos.

| ID    | Atributo      | Fuente             | Estímulo                                         | Artefacto           | Entorno                                    | Respuesta                                              | Medida                                               |
|-------|---------------|--------------------|--------------------------------------------------|----------------------|---------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| QA-01 | Rendimiento   | Sensor IoT         | Envía datos de temperatura y humedad             | Backend + Dashboard  | Operación normal con múltiples sensores activos | El sistema procesa y actualiza los datos en el dashboard | Actualización visible en menos de 10 segundos        |
| QA-02 | Confiabilidad | Sensor IoT         | Variación fuera del rango permitido              | Módulo de alertas    | Operación continua 24/7                     | El sistema genera y envía una notificación al usuario   | Notificación enviada en menos de 5 segundos          |
| QA-03 | Disponibilidad| Usuario            | Solicita acceso al dashboard                     | App web/móvil        | Acceso remoto desde cualquier ubicación     | El sistema permite visualizar inventario y estado       | Disponibilidad mayor o igual al 99 por ciento del tiempo |
| QA-04 | Escalabilidad | Múltiples usuarios | Consultas y monitoreo simultáneo de varias cavas | Backend central      | Alta concurrencia usuarios y sensores       | El sistema mantiene tiempos de respuesta estables       | Respuestas en menos de 3 segundos con múltiples usuarios |
| QA-05 | Seguridad     | Usuario            | Registro y almacenamiento de datos               | Base de datos        | Redes públicas WiFi, 4G, 5G                 | Los datos son almacenados y transmitidos de forma segura| 100 por ciento de datos protegidos mediante encriptación |



#### 4.1.2.3. Constraints.

En esta sección se presentan las restricciones del sistema, entendidas como condiciones no negociables establecidas por el cliente o por el negocio que sirven como lineamientos fundamentales para el desarrollo de la solución.

| ID     | Título                         | Descripción                                                                 | Aceptación                                                                 | EPIC  |
|--------|--------------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------|-------|
| CON-01 | Compatibilidad multiplataforma | La solución debe funcionar en dispositivos móviles y web para acceso remoto | Escenario 1: El usuario accede desde móvil y visualiza su inventario correctamente.<br>Escenario 2: El usuario accede desde web y los datos se muestran sincronizados. | EP01 |
| CON-02 | Integración con sensores IoT   | El sistema debe conectarse con sensores para monitoreo ambiental            | Escenario 1: El sensor envía datos y el sistema los recibe correctamente.<br>Escenario 2: El usuario visualiza los datos y estos se reflejan en el dashboard. | EP03 |
| CON-03 | Monitoreo en tiempo real       | El sistema debe procesar datos ambientales en tiempo casi real              | Escenario 1: El sensor envía datos y la actualización se realiza en menos de 10 segundos.<br>Escenario 2: Existen múltiples sensores activos y el sistema mantiene la actualización continua. | EP03 |
| CON-04 | Alertas inmediatas             | El sistema debe notificar cambios críticos de temperatura/humedad           | Escenario 1: Se supera el umbral y se envía una notificación.<br>Escenario 2: El usuario recibe la alerta y puede actuar rápidamente. | EP03 |
| CON-05 | Almacenamiento histórico       | El sistema debe guardar datos históricos para análisis                      | Escenario 1: El sistema registra datos continuamente y se almacenan correctamente.<br>Escenario 2: El usuario consulta el historial y visualiza gráficos sin errores. | EP04 |
| CON-06 | Arquitectura escalable         | La solución debe soportar múltiples usuarios y sensores simultáneamente     | Escenario 1: Varios usuarios acceden y el sistema responde sin caídas.<br>Escenario 2: Existen múltiples sensores activos y no se degrada el rendimiento. | EP03 |
| CON-07 | Seguridad de datos             | La información debe almacenarse y transmitirse de forma segura              | Escenario 1: El usuario registra datos y estos se almacenan encriptados.<br>Escenario 2: El usuario accede desde una red pública y la información se mantiene segura. | EP01 |
| CON-08 | Simplicidad de uso             | La aplicación debe ser fácil de usar y evitar procesos manuales complejos   | Escenario 1: El usuario registra una botella y el proceso es rápido.<br>Escenario 2: El usuario navega en la aplicación y la interfaz es intuitiva sin fricción. | EP02 |


#### 4.1.2.3. Constraints.

En esta sección se presentan las restricciones del sistema, entendidas como condiciones no negociables establecidas por el cliente o por el negocio que sirven como lineamientos fundamentales para el desarrollo de la solución.

| ID     | Título                         | Descripción                                                                 | Aceptación                                                                 | EPIC  |
|--------|--------------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------|-------|
| CON-01 | Compatibilidad multiplataforma | La solución debe funcionar en dispositivos móviles y web para acceso remoto | Escenario 1: El usuario accede desde móvil y visualiza su inventario correctamente.<br>Escenario 2: El usuario accede desde web y los datos se muestran sincronizados. | EP01 |
| CON-02 | Integración con sensores IoT   | El sistema debe conectarse con sensores para monitoreo ambiental            | Escenario 1: El sensor envía datos y el sistema los recibe correctamente.<br>Escenario 2: El usuario visualiza los datos y estos se reflejan en el dashboard. | EP03 |
| CON-03 | Monitoreo en tiempo real       | El sistema debe procesar datos ambientales en tiempo casi real              | Escenario 1: El sensor envía datos y la actualización se realiza en menos de 10 segundos.<br>Escenario 2: Existen múltiples sensores activos y el sistema mantiene la actualización continua. | EP03 |
| CON-04 | Alertas inmediatas             | El sistema debe notificar cambios críticos de temperatura/humedad           | Escenario 1: Se supera el umbral y se envía una notificación.<br>Escenario 2: El usuario recibe la alerta y puede actuar rápidamente. | EP03 |
| CON-05 | Almacenamiento histórico       | El sistema debe guardar datos históricos para análisis                      | Escenario 1: El sistema registra datos continuamente y se almacenan correctamente.<br>Escenario 2: El usuario consulta el historial y visualiza gráficos sin errores. | EP04 |
| CON-06 | Arquitectura escalable         | La solución debe soportar múltiples usuarios y sensores simultáneamente     | Escenario 1: Varios usuarios acceden y el sistema responde sin caídas.<br>Escenario 2: Existen múltiples sensores activos y no se degrada el rendimiento. | EP03 |
| CON-07 | Seguridad de datos             | La información debe almacenarse y transmitirse de forma segura              | Escenario 1: El usuario registra datos y estos se almacenan encriptados.<br>Escenario 2: El usuario accede desde una red pública y la información se mantiene segura. | EP01 |
| CON-08 | Simplicidad de uso             | La aplicación debe ser fácil de usar y evitar procesos manuales complejos   | Escenario 1: El usuario registra una botella y el proceso es rápido.<br>Escenario 2: El usuario navega en la aplicación y la interfaz es intuitiva sin fricción. | EP02 |
### 4.1.3. Architectural Drivers Backlog.

| Driver ID | Título          | Descripción                                                                                                                                 | Importancia | Complejidad Técnica |
|-----------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------|---------------------|
| DR-01     | Rendimiento    | Capacidad del sistema para procesar datos de sensores IoT y reflejarlos en el dashboard en menos de 10 segundos, así como generar alertas inmediatas ante variaciones críticas, garantizando monitoreo en tiempo casi real. | Alta        | Alta                |
| DR-02     | Disponibilidad | Capacidad del sistema para mantenerse operativo de forma continua 24/7, permitiendo a los usuarios acceder al estado de su cava y monitorear condiciones ambientales desde cualquier ubicación sin interrupciones. | Alta        | Media               |
| DR-03     | Seguridad      | Implementación de mecanismos de protección de datos, incluyendo almacenamiento seguro, comunicación encriptada y protección ante accesos no autorizados, garantizando la confidencialidad de la información del usuario y su colección. | Alta        | Media               |
| DR-04     | Usabilidad     | Capacidad del sistema para ofrecer una experiencia simple e intuitiva, permitiendo registrar botellas, consultar inventario y visualizar datos sin fricción, reduciendo la dependencia de procesos manuales. | Alta        | Media               |
| DR-05     | Escalabilidad  | Habilidad del sistema para soportar múltiples usuarios y sensores IoT simultáneamente, manteniendo tiempos de respuesta estables y sin degradación del servicio en escenarios de crecimiento. | Alta        | Alta                |
| DR-06     | Confiabilidad  | Garantía de funcionamiento consistente del sistema, asegurando la correcta recepción de datos de sensores y el envío de alertas sin pérdida de información, incluso en operación continua. | Media       | Alta                |
| DR-07     | Interoperabilidad | Capacidad del sistema para integrarse con dispositivos IoT, sensores ambientales y servicios externos, utilizando protocolos estándar y APIs para asegurar comunicación eficiente. | Media       | Media               |
| DR-08     | Modificabilidad | Facilidad para extender el sistema, incorporar nuevos sensores, mejorar funcionalidades y adaptar reglas de negocio sin afectar componentes existentes ni generar deuda técnica significativa. | Media       | Media               |


### 4.1.4. Architectural Design Decisions.

| Driver ID | Título          | Descripción                                                                                                                                 | Importancia | Complejidad Técnica |
|-----------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------|---------------------|
| DR-01     | Rendimiento    | Capacidad del sistema para procesar datos de sensores IoT y reflejarlos en el dashboard en menos de 10 segundos, así como generar alertas inmediatas ante variaciones críticas, garantizando monitoreo en tiempo casi real. | Alta        | Alta                |
| DR-02     | Disponibilidad | Capacidad del sistema para mantenerse operativo de forma continua 24/7, permitiendo a los usuarios acceder al estado de su cava y monitorear condiciones ambientales desde cualquier ubicación sin interrupciones. | Alta        | Media               |
| DR-03     | Seguridad      | Implementación de mecanismos de protección de datos, incluyendo almacenamiento seguro, comunicación encriptada y protección ante accesos no autorizados, garantizando la confidencialidad de la información del usuario y su colección. | Alta        | Media               |
| DR-04     | Usabilidad     | Capacidad del sistema para ofrecer una experiencia simple e intuitiva, permitiendo registrar botellas, consultar inventario y visualizar datos sin fricción, reduciendo la dependencia de procesos manuales. | Alta        | Media               |
| DR-05     | Escalabilidad  | Habilidad del sistema para soportar múltiples usuarios y sensores IoT simultáneamente, manteniendo tiempos de respuesta estables y sin degradación del servicio en escenarios de crecimiento. | Alta        | Alta                |
| DR-06     | Confiabilidad  | Garantía de funcionamiento consistente del sistema, asegurando la correcta recepción de datos de sensores y el envío de alertas sin pérdida de información, incluso en operación continua. | Media       | Alta                |
| DR-07     | Interoperabilidad | Capacidad del sistema para integrarse con dispositivos IoT, sensores ambientales y servicios externos, utilizando protocolos estándar y APIs para asegurar comunicación eficiente. | Media       | Media               |
| DR-08     | Modificabilidad | Facilidad para extender el sistema, incorporar nuevos sensores, mejorar funcionalidades y adaptar reglas de negocio sin afectar componentes existentes ni generar deuda técnica significativa. | Media       | Media               |

La arquitectura de Monolito Modular basada en Domain-Driven Design (DDD) se presenta como la alternativa más adecuada para el desarrollo de VineVault. Esta decisión se fundamenta en los siguientes aspectos:

En primer lugar, permite cumplir de manera efectiva con los drivers arquitectónicos definidos, especialmente en lo relacionado con el monitoreo en tiempo casi real de condiciones ambientales, la seguridad de los datos de los usuarios y la confiabilidad en la gestión del inventario de botellas.

Asimismo, reduce la complejidad operativa del sistema, lo cual resulta clave considerando que el proyecto está orientado a un entorno con recursos de desarrollo limitados. Una arquitectura monolítica modular facilita el desarrollo, despliegue y mantenimiento sin introducir sobrecarga innecesaria.

Por otro lado, esta arquitectura favorece la aplicación de Domain-Driven Design, permitiendo organizar el sistema en dominios claramente definidos como Inventario, Monitoreo IoT, Alertas y Análisis. Esto contribuye a una mejor estructuración del código y a una mayor coherencia con las necesidades del negocio.

Finalmente, evita la complejidad adicional que implicaría una arquitectura de microservicios, la cual, si bien es escalable, introduciría desafíos innecesarios en términos de comunicación entre servicios, despliegue distribuido y mantenimiento. Dado el alcance actual de VineVault, una solución monolítica modular resulta más eficiente, manejable y alineada con los requerimientos del sistema.

### 4.1.5. Quality Attribute Scenario Refinements.

![Scenario 01](../assets/Scenario-Refinements/Scenario01Refinement.png)

![Scenario 02](../assets/Scenario-Refinements/Scenario02Refinement.png)


## 4.2. Strategic-Level Domain-Driven Design.

Link del miro: https://miro.com/app/board/uXjVHXRgC6E=/?share_link_id=317409539991

### 4.2.1. EventStorming.

*Step 1: Unstructured Exploration*

Primero empezamos  con una lluvia de ideas de los eventos del dominio relacionados con el dominio empresarial que se está explorando. Un evento de dominio es algo interesante que ha sucedido en el negocio. Es importante formular eventos de dominio en tiempo pasado; están describiendo cosas que ya han sucedido.

<a href="https://ibb.co/g2DGZ6f"><img src="https://i.ibb.co/CcnqKWY/Untitled-5.jpg" alt="Step 1" border="0"></a>


En esta etapa se buscó entender qué situaciones importantes ocurren dentro de una cava inteligente. A diferencia de un inventario tradicional, el dominio de VineVault involucra no solo almacenamiento de botellas, sino también monitoreo ambiental, trazabilidad y conservación de vinos premium.


*Step 2: Timelines*

Ahora revisamos  los eventos de dominio generados y los organizan en el orden en que ocurren en el dominio empresarial. Los eventos deben comenzar con el happy path: el flujo que describe un escenario empresarial exitoso.

<a href="https://ibb.co/rfFhvdXk"><img src="https://i.ibb.co/YTPSb0V2/Untitled-6.jpg" alt="Untitled-6" border="0"></a>

La línea temporal permitió visualizar el ciclo de vida de una botella dentro de la cava:

1. El usuario crea su cava.
2. Registra botellas.
3. Vincula sensores IoT.
4. El sistema monitorea temperatura y humedad.
5. Se generan alertas.
6. El usuario consume o retira botellas.
7. El sistema analiza patrones históricos.

Esto ayudó a entender cómo interactúan las operaciones físicas de la cava con los procesos digitales y analíticos del sistema.


*Step 3: Paint Points*

Ahora veremos que todos los eventos organizados en una línea de tiempo, use esta vista amplia para identificar
puntos en el proceso que requieren atención. Estos pueden ser cuellos de botella, pasos manuales que
requieren automatización, documentación faltante o conocimiento de dominio faltante.
<a href="https://ibb.co/B59fVH7F"><img src="https://i.ibb.co/bMk6gjyD/Untitled-7.jpg" alt="Untitled-7" border="0"></a>


Durante el análisis se detectaron problemas frecuentes en la gestión manual de colecciones de vino:

1. Ingreso a la web fallida
2. Desconocimiento del estado ambiental de la cava.
3. Deterioro de vinos por cambios de temperatura.
4. Falta de alertas tempranas.
5. Dificultad para poder pagar la suscripcion 


Estos pain points justificaron la necesidad de automatizar el monitoreo y digitalizar la administración de la cava mediante IoT y análisis inteligente.

*Step 4: Pivotal Points*

En esta Seccion buscamos eventos comerciales importantes que indiquen un cambio en el contexto o la fase. Estos se denominan eventos fundamentales y están marcados con una barra vertical que divide los eventos antes y después del evento fundamental. 
<a href="https://ibb.co/twnt3tSv"><img src="https://i.ibb.co/V0bZ3Zdz/Untitled-8.jpg" alt="Untitled-8" border="0"></a>

Los eventos pivote ayudaron a descubrir cambios de responsabilidad y futuros bounded contexts.

1.- el usuario se registro
2.- el usuario ingreso 
3.- el usuario creo una cava 
3.- desea conectar el sensor
4.- crea un cava inteligente
5.- y por ultimo decie apliar funciones atravez de pago 

Estos eventos permitieron identificar separaciones naturales entre inventario, monitoreo ambiental y análisis inteligente.

*Step 5: Commands*

Ahora en  los comandos que describe qué desencadenó el evento o el flujo de eventos. Los comandos describen las operaciones del sistema y, contrariamente a los eventos de dominio, se formulan en imperativo.
<a href="https://ibb.co/3gC0xNz"><img src="https://i.ibb.co/rDwZB6s/Untitled-9.jpg" alt="Untitled-9" border="0"></a>

Los comandos modelaron las operaciones críticas del negocio:

- Register Bottle
- Connect Sensor
- Validate Environmental Ranges
- Generate Alert
- Remove Bottle From Inventory
- Generate Consumption Report

Esto permitió diferenciar claramente entre:

- acciones del usuario,automatizaciones del sistema, y respuestas del dominio.

También ayudó a descubrir agregados responsables de mantener la consistencia del negocio.

*Step 6: Policies*

Seguimos con agregar  al modelo, pero no tienen un actor específico asociado con ellos. Durante este paso, busca automation policies que puedan ejecutar esos comandos. Una automation policy un escenario en el que un evento desencadena la ejecución de un comando. En otras palabras, un comando se ejecuta automáticamente cuando ocurre un evento de dominio específico


<a href="https://ibb.co/mVyDfPGx"><img src="https://i.ibb.co/HfPF59VJ/Untitled-10.jpg" alt="Untitled-10" border="0"></a>

Las políticas reflejan automatizaciones fundamentales para una cava inteligente.

Ejemplos:

1. Si la temperatura supera el umbral permitido → generar alerta.
2. Si el stock de botellas es bajo → enviar advertencia.
3. Si el sensor deja de transmitir datos → marcar dispositivo inactivo.

Estas políticas permitieron entender que VineVault funciona como un sistema reactivo orientado a eventos y monitoreo continuo.

*Step7: ReadModels*

continuamos con Un modelo de lectura es la vista de datos dentro del dominio que el actor usa para tomar la decisión de ejecutar un comando. Puede ser una de las pantallas del sistema, un informe, una notificación, etc..

<a href="https://ibb.co/MDdxt5W3"><img src="https://i.ibb.co/pvqBMrG9/Untitled-11.jpg" alt="Untitled-11" border="0"></a>

Los read models permitieron visualizar cómo el usuario interactúa con la información de la cava.

Se identificaron vistas como:

1. Dashboard ambiental en tiempo real.
2. Inventario de botellas.
3. Historial de temperatura y humedad.
4. Reporte de consumo.
5. Recomendaciones de maduración.

Esto ayudó a validar qué información necesita cada actor para operar correctamente la cava.

*Step 8: External Systems*


Seguimos con los servicio externos este paso consiste en aumentar el modelo con sistemas externos. Un sistema externo se define como cualquier sistema que no forma parte del dominio que se está explorando. Puede ejecutar comandos (entrada) o puede ser notificado sobre eventos (salida).





<a href="https://ibb.co/Kp4rRRnx"><img src="https://i.ibb.co/PvX633kG/Untitled-12.jpg" alt="Untitled-12" border="0"></a>

El dominio depende de integraciones externas para operar correctamente.

Se identificaron:

1. Sensores IoT ESP32.
2. Servicio de correo electrónico.
3. Servicio de notificaciones push.
4. APIs externas para información de vinos (si aplica).

Esto permitió delimitar qué componentes pertenecen al dominio central y cuáles son dependencias externas.

*Step 9: Aggregates*

Una vez que todos los eventos y comandos están representados, los participantes pueden comenzar a pensar en organizar conceptos relacionados en agregados. Un agregado recibe comandos y produce eventos.

<a href="https://ibb.co/kvXSC36"><img src="https://i.ibb.co/mg4cWvF/Untitled-13.jpg" alt="Untitled-13" border="0"></a>

Los agregados permitieron mantener consistencia en las operaciones críticas del dominio.

Se identificaron agregados como:

- wine catalog
- user sesion 
- sensor device
- notification request
- Inventory Analitycs
- suscription 


Esto ayudó a descubrir límites naturales de consistencia y fue la base para definir posteriormente los Bounded Contexts.

### 4.2.2. Candidate Context Discovery.

*Step 10: Bounded Contexts*

El último paso de una sesión de tormenta de eventos es buscar agregados que estén relacionados entre sí, ya sea porque representan una funcionalidad estrechamente relacionada o porque están acoplados a través de políticas. Los grupos de agregados forman candidatos naturales para los límites de los contextos delimitados.

<a href="https://ibb.co/M5RPNvqy"><img src="https://i.ibb.co/84jP8CFn/Event-Storming-Vine-Vault.jpg" alt="Event-Storming-Vine-Vault" border="0"></a>

Durante la sesión, el equipo ejecutó las siguientes actividades:

1. **Descubrimiento de Domain Events (post-its naranjas):** Se identificaron los eventos más relevantes del negocio, tales como `User Registered`, `Wine Created`, `Sensor Activated`, `Alert Threshold Exceeded`, `Monthly Report Generated`, entre otros. Estos se dispusieron en orden cronológico sobre una línea de tiempo horizontal.

2. **Identificación de Actores y Sistemas Externos (post-its azules y rosas):** Se agregaron los usuarios (`Collector`, `Admin`), los sistemas externos (`Payment Gateway`, `Email Service`) y las políticas de negocio que disparan acciones automáticas.

3. **Comandos y Agregados (post-its amarillos y verdes):** Para los flujos más críticos, se modelaron los comandos que desencadenan los eventos y los agregados responsables de mantener la consistencia.

4. **Validación de la narrativa:** Se recorrió la línea de tiempo completa verificando que cada evento tuviera un origen lógico (comando o política) y un consumidor claro, eliminando ambigüedades en el lenguaje.



#### Técnicas aplicadas

Se aplicaron las siguientes técnicas durante la sesión:

#### a) Start-with-value

Se identificaron las partes del dominio que aportan mayor valor diferencial al negocio:

- **Inventory Intelligence:** Es el *core domain*, ya que la recomendación predictiva y el análisis de consumo son la propuesta de valor principal frente a competidores.
- **Environmental Monitoring:** Es un *supporting domain* crítico, ya que la monitorización en tiempo real justifica la suscripción Premium.

#### b) Start-with-simple

En lugar de intentar diseñar todos los contextos a la vez, se descompuso la línea de tiempo del EventStorm en pasos secuenciales simples:

1. El usuario se registra → **IAM**
2. El usuario crea su cava y añade vinos → **Wine Catalog**
3. El sistema conecta sensores y monitorea → **Environmental Monitoring**
4. Si hay desviaciones, se notifica → **Notification**
5. El usuario paga por el servicio → **Subscription / Billing**
6. El sistema analiza patrones y recomienda → **Inventory Intelligence**

#### c) Look-for-pivotal-events

Se buscaron eventos clave que indicaran cambios de estado y, por tanto, cambios de modelo:

- **`User Registered`** → separa el mundo externo (registro) del dominio interno (gestión de la cava).
- **`Sensor Activated`** → marca el paso de la gestión manual de inventario a la monitorización automatizada.
- **`Alert Threshold Exceeded`** → evento pivote que conecta el dominio de monitorización con el de notificaciones.
- **`Subscription Upgraded`** → delimita el contexto de facturación del contexto de catálogo de vinos.

#### Bounded Contexts identificados

Como resultado de la sesión, se definieron los siguientes **Bounded Contexts candidatos**:

| Bounded Context | Tipo (Core/Generic/Supporting) | Descripción |
|---|---|---|
| **IAM** | Generic | Gestión de identidad, autenticación, autorización y perfiles de usuario. |
| **Wine Catalog** | Core domain | Administración del inventario físico: añadir, clasificar, consumir y valorizar los vinos de la cava. |
| **Environmental Monitoring** | Supporting | Gestión de dispositivos IoT, lecturas de sensores y evaluación de condiciones ambientales. |
| **Notification** | Generic | Emisión de alertas, recordatorios y reportes a través de múltiples canales (email, push). |
| **Subscription & Billing** | Supporting | Gestión de planes de suscripción, pagos recurrentes y control de acceso a funcionalidades Premium. |
| **Inventory Intelligence** | Core domain | Motor analítico que genera reportes de consumo, predicciones de maduración y recomendaciones de compra. |

## Relaciones entre contextos

Se identificaron las siguientes relaciones de colaboración:

- **IAM → Wine Catalog:** IAM publica `User Registered` / `User Authenticated` que el catálogo consume para crear perfiles de coleccionista.
- **Wine Catalog → Inventory Intelligence:** El catálogo alimenta datos de inventario al motor analítico.
- **Environmental Monitoring → Notification:** Cuando se excede un umbral, se emite un `Alert Triggered` que el contexto de notificaciones procesa.
- **Subscription → Wine Catalog / Environmental Monitoring:** El nivel de suscripción determina qué funcionalidades (cantidad de vinos, número de sensores) están disponibles.

### 4.2.3. Domain Message Flows Modeling.

A partir del análisis del modelo de dominio, se han identificado y modelado flujos de mensajes críticos que describen la interacción entre los diferentes actores, sistemas externos y los Bounded Contexts. Estos escenarios validan cómo la información fluye para cumplir los objetivos de negocio:

<a href="https://ibb.co/5gdbG2Jp"><img src="https://i.ibb.co/FL9RmndZ/Event-Storming-Vine-Vault-1.jpg" alt="Event-Storming-Vine-Vault-1" border="0"></a>

**Scenario: User Registration and Access Activation:**

1. El flujo inicia cuando un User interactúa con el Website para registrarse enviando los datos correspondientes (email y password).

2. El comando Register User se envía al contexto IAM.

3. IAM emite el evento de dominio User registered.

4. El sistema valida la cuenta y se emite el comando Send Verification Email, que es manejado por un Email Service (sistema externo) para enviar el correo al usuario.

5. Una vez que el usuario verifica su correo a través de la interfaz web (Verify User Email), IAM emite el evento User Email verified.

6. Este evento es crucial, ya que dispara la creación inicial de la cava en el contexto WINE INVENTORY (Create initial cava), almacenando la información de manera persistente.

<a href="https://ibb.co/hRhggGyT"><img src="https://i.ibb.co/GvBddZ0r/Event-Storming-Vine-Vault-2.jpg" alt="Event-Storming-Vine-Vault-2" border="0"></a>

**Scenario: Bottle Registration & connect to IoT:**

1. El User ingresa una nueva botella mediante el Website ejecutando el comando Register new Bottle.

2. El comando es procesado por el contexto WINE INVENTORY.

3. Se genera el evento Bottle registered.

4. El inventario sincroniza esta nueva entrada con el estado del sistema IoT (SYNCHRONIZED IoT), vinculando el ID de la botella y de la cava.

<a href="https://ibb.co/QjjdtKgg"><img src="https://i.ibb.co/FqqVCDrr/Event-Storming-Vine-Vault-3.jpg" alt="Event-Storming-Vine-Vault-3" border="0"></a>

**Scenario: Real-Time Environmental Alert & Notification:**

1. El sensor IoT (Sensor ESP32) envía datos telemétricos (Push Telemetry Data) continuamente al contexto Environmental Monitoring.

2. Este contexto ejecuta una lógica interna para validar los rangos ambientales (Validate Environmental Ranges).

3. Si se detecta una anomalía, se emite el evento Critical Temperature Alert Detected.

4. Este evento es consumido por el contexto Notification, el cual procesará y enviará la alerta al usuario (como se definió en el Context Map a través de eventos publicados).


<a href="https://ibb.co/93SrSb8v"><img src="https://i.ibb.co/2YHkHvn6/Event-Storming-Vine-Vault-4.jpg" alt="Event-Storming-Vine-Vault-4" border="0"></a>

**Scenario: Bottle Removal & Consumption Tracking:**

1. El usuario (Home User / Sommelier) retira una botella ejecutando el comando Remove Bottle from Inventory sobre el contexto WINE INVENTORY.

3. Se emite el evento de dominio Bottle Consumption Registered.

4. Este evento desencadena un Bottle Consumption Report que es procesado por el contexto de análisis, Inventory Intelligence.

5. Si el stock remanente es bajo, el contexto de análisis emite el comando Send Low Stock Warning hacia el contexto Notification.

6. Finalmente, Notification envía la alerta (Low Stock Warning Sent) al usuario.

### 4.2.4. Bounded Context Canvases.

<a href="https://ibb.co/C3xRZHBt"><img src="https://i.ibb.co/JwXD4snd/Event-Storming-Vine-Vault.jpg" alt="Event-Storming-Vine-Vault" border="0"></a>

**Explicacion:** Identity & Access Management (IAM) - Generic Subdomain: Este contexto se encarga de la gestión del ciclo de vida del usuario, la autenticación y la autorización basada en roles. Es un subdominio genérico porque, aunque es vital para la seguridad y el multitenancy, no representa la ventaja competitiva principal del sistema.

<a href="https://ibb.co/fdqMgCGv"><img src="https://i.ibb.co/whBykKrs/Event-Storming-Vine-Vault-1.jpg" alt="Event-Storming-Vine-Vault-1" border="0"></a>

**Explicacion:** Wine  Inventory - Core Domain: Representa el corazón del sistema. Es responsable de mantener la integridad física y lógica del inventario de botellas. Aquí reside el Lenguaje Ubicuo crítico como "Bottle Instance", "Wine Profile" y las reglas de trazabilidad obligatoria. Al ser el núcleo operativo, requiere la mayor inversión de esfuerzo arquitectónico.

<a href="https://ibb.co/5XHKHFWy"><img src="https://i.ibb.co/HL8h8dDs/Event-Storming-Vine-Vault-2.jpg" alt="Event-Storming-Vine-Vault-2" border="0"></a>

**Explicacion:** Environmental Monitoring - Supporting Domain: Su propósito es capturar, validar y persistir los flujos de datos (telemetría) provenientes de los sensores IoT físicos (temperatura y humedad). Maneja conceptos como "Threshold", "Environmental Drift" y "Heartbeat". Da soporte al Core Domain al proveer los datos crudos del entorno de la cava.

<a href="https://ibb.co/ymcmqcGN"><img src="https://i.ibb.co/xKtK6tP2/Event-Storming-Vine-Vault-3.jpg" alt="Event-Storming-Vine-Vault-3" border="0"></a>

**Explicacion:** Inventory Intelligence - Core Domain: Este es el motor analítico diferencial de VineVault. Transforma los datos históricos de inventario y la telemetría en insights accionables, como predicciones de maduración y recomendaciones de consumo.

<a href="https://ibb.co/nqmMDjpY"><img src="https://i.ibb.co/Fk34Bzpy/Event-Storming-Vine-Vault-4.jpg" alt="Event-Storming-Vine-Vault-4" border="0"></a>

**Explicacion:** Centraliza la lógica de despacho de mensajes (alertas térmicas, reportes mensuales) hacia los usuarios finales a través de múltiples canales (Email, Push). 

### 4.2.5. Context Mapping.

Una vez identificados los seis Bounded Contexts candidatos durante la sesión de *Candidate Context Discovery*, el equipo realizó un ejercicio de **Context Mapping** con el objetivo de definir las relaciones estructurales entre ellos. Este proceso permitió visualizar cómo los contextos colaboran, qué dependencias existen y qué patrones de integración de Domain-Driven Design resultan más apropiados para mantener la autonomía de cada modelo sin sacrificar la cohesión del sistema.

Para cada relación potencial entre Bounded Contexts, el equipo discutió las siguientes preguntas de diseño:

| Pregunta de diseño | Contexto aplicado | Conclusión del equipo |
|---|---|---|
| *¿Qué pasaría si movemos este capability a otro bounded context?* | ¿Mover la gestión de umbrales de alerta de **Environmental Monitoring** a **Notification**? | Rechazado. El umbral es lógica de dominio del sensor, no del canal de notificación. |
| *¿Qué pasaría si descomponemos este capability y movemos uno de los sub-capabilities a otro bounded context?* | ¿Separar la clasificación de vinos (uva, región, año) del **Wine Catalog** hacia **Inventory Intelligence**? | Rechazado. La clasificación es parte del lenguaje del coleccionista; el catálogo debe mantenerla. |
| *¿Qué pasaría si partimos el bounded context en múltiples bounded contexts?* | ¿Dividir **Subscription & Billing** en dos: uno para planes y otro para pagos? | Rechazado. Ambos comparten el mismo lenguaje de "suscripción activa" y el ciclo de vida está acoplado. |
| *¿Qué pasaría si tomamos este capability de estos 3 contexts y lo usamos para formar un nuevo context?* | ¿Extraer la validación de permisos de IAM, Wine Catalog y Environmental Monitoring hacia un nuevo **Authorization Context**? | Rechazado. Sobre-diseño. IAM ya cubre identidad; duplicaría esfuerzos. |
| *¿Qué pasaría si duplicamos una funcionalidad para romper la dependencia?* | ¿Duplicar el cálculo de "vino disponible" en **Wine Catalog** y **Inventory Intelligence**? | Parcialmente aceptado. Intelligence mantiene su propia vista de lectura (CQRS) para reportes, pero la fuente de verdad permanece en Wine Catalog. |
| *¿Qué pasaría si creamos un shared service para reducir la duplicación entre múltiples bounded contexts?* | ¿Crear un servicio compartido de plantillas de email para **Notification** y **Subscription & Billing**? | Rechazado. Notification es genérico y puede absorber la responsabilidad sin acoplarse a facturación. |
| *¿Qué pasaría si aislamos los core capabilities y movemos los otros a un context aparte?* | ¿Mover el historial de lecturas de sensores de **Environmental Monitoring** a un contexto de Data Lake? | Rechazado para MVP. Aceptado como evolución futura si el volumen de datos IoT crece. |


##### Diagrama de Context Mapping 

<a href="https://ibb.co/yc7BBMfJ"><img src="https://i.ibb.co/cSVXXpgd/Captura-de-pantalla-2026-05-14-162217.png" alt="Captura-de-pantalla-2026-05-14-162217" border="0"></a>

##### 1. Wine Catalog → Inventory Intelligence: **Conformist**
- **Upstream:** Wine Catalog
- **Downstream:** Inventory Intelligence
- **Decisión:** Intelligence se conforma al modelo Wine del catálogo
- **Rationale:** Duplicar el modelo generaría inconsistencias en reportes analíticos

##### 2. IAM → Wine Catalog: **Customer/Supplier**
- **Upstream:** IAM
- **Downstream:** Wine Catalog
- **Decisión:** IAM es supplier de autenticación y roles
- **Rationale:** El catálogo no debe gestionar su propia autenticación


##### 3. Subscription & Billing → Wine Catalog: **Customer/Supplier**
- **Upstream:** Subscription & Billing
- **Downstream:** Wine Catalog
- **Decisión:** Subscription define límites de capacidad
- **Rationale:** La definición de "qué incluye cada plan" es regla de negocio de marketing

##### 4. IAM → Inventory Intelligence: **Customer/Supplier**
- **Upstream:** IAM
- **Downstream:** Intelligence
- **Decisión:** IAM provee autenticación centralizada
- **Rationale:** Los reportes contienen datos sensibles; la autorización debe ser auditada

##### 5. Environmental Monitoring → Inventory Intelligence: **Anti-Corruption Layer (ACL)**
- **Upstream:** Environmental Monitoring
- **Downstream:** Intelligence
- **Decisión:** ACL traduce eventos técnicos de IoT a modelo de dominio
- **Rationale:** Protege el modelo analítico de la volatilidad del hardware IoT

##### 6. Inventory Intelligence → Notification: **Published Events** (asíncrono)
- **Patrón:** Eventos publicados
- **Rationale:** Reportes batch no deben bloquearse por retrasos en Notification

##### 7. Environmental Monitoring → Notification: **Published Events** (asíncrono)
- **Patrón:** Eventos publicados
- **Rationale:** IoT no debe gestionar plantillas de email ni reintentos

##### 8. Subscription & Billing → Notification: **Conformist**
- **Upstream:** Subscription & Billing
- **Downstream:** Notification
- **Rationale:** El email de facturación es la fuente de verdad del contacto

##### 9. IAM → Notification: **Customer/Supplier**
- **Upstream:** IAM
- **Downstream:** Notification
- **Rationale:** Notification necesita roles para filtrar alertas

##### 10. IAM ↔ Subscription & Billing: **Shared Kernel**
- **Patrón:** Compartido acotado a User Identity & Permissions
- **Rationale:** Ninguno puede imponer su ritmo al otro; cambios requieren aprobación conjunta

##### 11. Subscription & Billing → IAM: **Customer/Supplier**
- **Upstream:** Subscription & Billing
- **Downstream:** IAM
- **Rationale:** Subscription define qué permisos son "premium"


##### Resumen de Patrones

| Relación | Patrón |
|----------|--------|
| Wine Catalog → Intelligence | Conformist |
| IAM → Wine Catalog | Customer/Supplier |
| Subscription → Wine Catalog | Customer/Supplier |
| IAM → Intelligence | Customer/Supplier |
| Environmental Monitoring → Intelligence | ACL |
| Intelligence → Notification | Published Events |
| Environmental Monitoring → Notification | Published Events |
| Subscription → Notification | Conformist |
| IAM → Notification | Customer/Supplier |
| IAM ↔ Subscription | Shared Kernel |
| Subscription → IAM | Customer/Supplier |


## 4.3. Software Architecture.

### 4.3.1. Software Architecture System Landscape Diagram.

<a href="https://ibb.co/KcVnhRyK"><img src="https://i.ibb.co/BHTk3dsn/vinevault-dark-1.png" alt="vinevault-dark-1" border="0"></a>


##### Descripción General

VineVault es una plataforma centralizada de gestión de bodegas de vino que integra monitoreo IoT, control de inventario y análisis impulsado por IA generativa. La arquitectura implementa un modelo de capas con clara separación de responsabilidades entre presentación, integración, lógica de negocio, persistencia e IoT.

##### Actores del Sistema

**Facility Admin**: Operador de bodega comercial/restaurante que gestiona múltiples sensores, controla inventario y analiza rotación de ventas.

**Home User**: Coleccionista privado que monitorea su colección personal, recibe recomendaciones de consumo y supervisa condiciones ambientales.

**Support & Maintenance Team**: Equipo interno que gestiona tickets, resuelve incidencias y coordina mantenimiento del producto.

##### Plataforma VineVault - Arquitectura Interna

| Componente | Tecnología | Responsabilidad |
|---|---|---|
| **Landing Page** | HTML/CSS/JavaScript | Presentación pública de la plataforma |
| **Web App** | Vue 3 | Aplicación web autenticada para usuarios |
| **SPA** | Vue 3 | Experiencia cliente con widget de soporte embebido |
| **API Gateway** | Spring Cloud Gateway | Enrutamiento, rate limiting, seguridad básica |
| **Platform API** | Spring Boot/Java 25 | Lógica de negocio: IAM, Billing, Inventario, Monitoreo, IA, Notificaciones, Integraciones |
| **PostgreSQL DB** | PostgreSQL | Persistencia: usuarios, botellas, telemetría, suscripciones, logs integraciones |
| **ESP32 Device** | C/C++ Firmware | Medición de temperatura/humedad, envío de telemetría vía Wi-Fi |

##### Sistemas Externos - Core Business

| Sistema | Tipo | Protocolo | Función |
|---|---|---|---|
| **Google OAuth2** | Autenticación | OpenID Connect | Login social seguro |
| **Stripe** | Pagos | REST API/HTTPS | Procesamiento de pagos y suscripciones |
| **Resend** | Notificaciones | REST API/HTTPS | Emails transaccionales (verificación, alertas, reportes) |
| **ESP32 Hardware** | IoT | MQTT/HTTPS | Sensores físicos en celda |

#### Inteligencia Artificial Generativa

**Servicio**: OpenAI GPT / Anthropic Claude / Google Gemini

**Entrada**: Métricas de inventario, patrones de consumo, telemetría ambiental

**Salida**: Recomendaciones inteligentes, predicciones de madurez, reportes en lenguaje natural, análisis de tendencias

**Protocolo**: REST API/HTTPS

##### Sistemas de Inventario Externos (Integración)

| Sistema | Protocolo | Capacidad |
|---|---|---|
| **QuickBooks** | REST API/HTTPS | Sincronización finanzas y existencias |
| **Odoo** | REST API/HTTPS | Intercambio inventario y catálogo |
| **Zoho Inventory** | REST API/HTTPS | Actualizaciones stock y registros botellas |

**Patrón**: Sincronización bidireccional programada o disparada por eventos.

##### Soporte y Mantenimiento

**Ticketing System** (Zendesk/Freshdesk/Jira Service Management):
- Widget embebido en SPA para crear/rastrear tickets
- Protocolo: HTTPS/Widget API
- Notificación automática a Support Team

**Flujo**: Usuario crea ticket → Sistema notifica equipo → Support Team resuelve → Usuario recibe actualizaciones en VineVault.

##### Flujos Principales de Datos

##### Autenticación
Usuario → Landing Page → Google OAuth2 → API Gateway → Platform API
→ PostgreSQL (verificación) → Sesión iniciada

##### Monitoreo Ambiental
ESP32 Device → Sensores → Telemetría (MQTT/HTTPS) → API Gateway
→ Platform API → PostgreSQL + IA Service → Notificación usuario (Resend)

##### Procesamiento de Pagos
SPA → API Gateway → Stripe → Webhook → Platform API → PostgreSQL
→ Email confirmación (Resend)

##### Recomendaciones IA
Platform API → Recopila datos (inventario, consumo, telemetría)
→ Generative AI Service → Análisis + Predicciones → PostgreSQL → SPA

##### Integración de Inventario
Platform API → Sincronización bidireccional
→ QuickBooks/Odoo/Zoho Inventory → PostgreSQL (actualiza registros)

##### Arquitectura de Capas

| Capa | Componentes | Ubicación | Responsabilidad |
|---|---|---|---|
| **Presentación** | Landing Page, Web App, SPA | Navegador cliente | Interfaz usuario e interactividad |
| **Integración** | API Gateway | Backend | Enrutamiento, seguridad, rate limiting |
| **Lógica de Negocio** | Platform API | Backend | Procesamiento reglas negocio y orquestación |
| **Persistencia** | PostgreSQL | Backend | Almacenamiento ACID y recuperación datos |
| **IoT** | ESP32 Device | Celda física | Captura datos ambientales |

##### Principios de Diseño

- **Separación de responsabilidades**: Cada capa independiente con interfaz clara.
- **Escalabilidad horizontal**: API Gateway y Platform API sin estado, desplegables en Kubernetes.
- **Seguridad por capas**: OpenID Connect + HTTPS + API Keys + rate limiting.
- **Integraciones desacopladas**: APIs REST bidireccionales, sin dependencias críticas.
- **Observabilidad**: Logs centralizados, métricas y alertas sobre fallos sensor, errores API, caídas servicio.

##### Alineación Estratégica

Esta arquitectura soporta los objetivos estratégicos:

- **Diferenciación**: IA integrada para recomendaciones inteligentes
- **Escalabilidad**: Soporte simultáneo de usuarios domésticos y comerciales
- **Confiabilidad**: Monitoreo en tiempo real con alertas automáticas
- **Extensibilidad**: Nuevos sensores, integraciones y proveedores IA sin rediseño
- **Operacionalidad**: Gestión de soporte integrada, mantenimiento sin disrupciones



### 4.3.2. Software Architecture Context Level Diagrams.

<a href="https://ibb.co/RT9TG1nF"><img src="https://i.ibb.co/whRhZTHk/Vine-Vault-System-Context-dark.png" alt="Vine-Vault-System-Context-dark" border="0"></a>

#### Descripción General

El diagrama de contexto del sistema representa la vista de más alto nivel de la plataforma VineVault, mostrando los límites del sistema, los actores externos que interactúan con él y las principales relaciones de comunicación. Esta vista establece el contexto en el que opera la plataforma dentro del ecosistema empresarial.

#### Actores del Sistema (Personas)

##### Facility Admin
**Rol**: Propietario u operador de bodega comercial, restaurante o instalación con múltiples sensores y botellas.

**Interacciones con VineVault**:
- Gestión de bodega comercial con múltiples sensores
- Monitoreo de temperatura y humedad en tiempo real
- Control de inventario de botellas
- Visualización de análisis de rotación y ventas
- Acceso a reportes y analytics avanzados

**Acceso a soporte**:
- Crea y rastrea tickets de soporte mediante widget embebido en la aplicación

##### Home User
**Rol**: Entusiasta del vino o coleccionista privado propietario de una bodega personal.

**Interacciones con VineVault**:
- Gestión de colección personal de vino
- Monitoreo de condiciones ambientales de su celda
- Recepción de recomendaciones de consumo inteligentes
- Acceso a información de madurez del vino

**Acceso a soporte**:
- Crea y rastrea tickets de soporte mediante widget embebido en la aplicación

##### Support & Maintenance Team
**Rol**: Equipo interno responsable de gestionar tickets, atender inquietudes y coordinar mantenimiento del producto.

**Interacciones**:
- Recibe notificaciones de nuevos tickets y escalaciones desde el sistema de ticketing
- Revisa, gestiona y resuelve tickets dentro de la plataforma externa
- Realiza mantenimiento, troubleshooting y soporte técnico directo en VineVault
- Coordina actualizaciones y mejoras del producto

##### Sistema Central: VineVault Platform

**Propósito**: Plataforma centralizada para monitoreo, control y automatización de dispositivos de bodega de vino e inventario.

**Capacidades principales**:
- Autenticación y gestión de identidad de usuarios
- Procesamiento de pagos y gestión de suscripciones
- Catálogo de vinos e inventario de botellas
- Monitoreo ambiental en tiempo real (temperatura/humedad)
- Análisis inteligente con recomendaciones impulsadas por IA
- Gestión centralizada de notificaciones y alertas
- Integración bidireccional con sistemas de inventario externos
- Exportación de datos en múltiples formatos

#### Sistemas Externos - Autenticación y Pagos

##### Google OAuth2
**Tipo**: Servicio externo de autenticación

**Protocolo**: OpenID Connect

**Función**: Proporciona autenticación segura mediante login social. Los usuarios pueden acceder a VineVault utilizando sus credenciales de Google sin crear contraseñas separadas.

**Flujo de interacción**:
- VineVault → Delega verificación de identidad a Google
- Google → Verifica credenciales y devuelve token JWT
- VineVault → Recibe y valida token, inicia sesión de usuario

##### Stripe
**Tipo**: Plataforma de procesamiento de pagos

**Protocolo**: REST API / Webhooks

**Función**: Procesa pagos de suscripción, gestiona ciclos de facturación, mantiene historial de transacciones e informa cambios de estado mediante webhooks.

**Flujo de interacción**:
- VineVault → Crea sesión de checkout cuando usuario selecciona plan
- Stripe → Procesa pago y retorna confirmación
- Stripe → Envía webhook de confirmación de pago a VineVault
- VineVault → Actualiza suscripción del usuario basado en webhook

##### Resend
**Tipo**: Plataforma de entrega de emails transaccionales

**Protocolo**: REST API

**Función**: Envía emails de verificación de cuenta, recuperación de contraseña, alertas de condiciones críticas y reportes periódicos a usuarios.

**Flujo de interacción**:
- VineVault → Envía solicitud de email con contenido y destinatario
- Resend → Entrega email al destinatario
- Resend → Confirma estado de entrega a VineVault

#### Sistemas Externos - IoT y Hardware

##### ESP32 Hardware
**Tipo**: Dispositivo físico IoT

**Ubicación**: Instalado dentro de la bodega de vino

**Función**: Sensores que capturan datos ambientales en tiempo real.

**Capacidades**:
- Medición continua de temperatura
- Medición continua de humedad relativa
- Almacenamiento temporal de lecturas
- Conectividad Wi-Fi integrada

##### ESP32 Sensor Device (VineVault)
**Tipo**: Firmware embebido que ejecuta en el dispositivo ESP32

**Tecnología**: C/C++

**Función**: Software que normaliza lecturas de sensores, valida rangos seguros y publica telemetría a la plataforma cloud.

**Protocolo**: MQTT/HTTPS

**Flujo de interacción**:
- ESP32 Device → Captura mediciones del hardware
- ESP32 Device → Valida rangos seguros
- ESP32 Device → Envía telemetría a API Gateway
- VineVault → Recibe telemetría
- VineVault → Envía comandos de configuración al dispositivo

#### Sistemas Externos - Inteligencia Artificial

##### Generative AI Service
**Tipo**: Servicio externo de IA generativa

**Proveedores soportados**: OpenAI GPT, Anthropic Claude, Google Gemini

**Protocolo**: REST API / HTTPS

**Función**: Genera recomendaciones inteligentes basadas en datos de la bodega, predice madurez de vinos, crea reportes en lenguaje natural e identifica patrones de consumo.

**Datos de entrada**:
- Métricas de inventario (cantidad de botellas, valor, antigüedad)
- Patrones de consumo (botellas uncorkidas por período)
- Telemetría ambiental (historial de temperatura/humedad)

**Salida generada**:
- Recomendaciones personalizadas de cuándo consumir vinos específicos
- Predicciones de madurez óptima para botellas
- Análisis de tendencias de consumo del usuario
- Reportes narrativos de rotación de stock

**Flujo de interacción**:
- VineVault → Recopila datos contextuales (inventario, consumo, telemetría)
- VineVault → Envía prompt estructurado a IA con contexto
- IA → Procesa datos y genera insights
- IA → Devuelve recomendaciones
- VineVault → Almacena resultados y los expone al usuario

#### Sistemas Externos - Integración de Inventario

#### QuickBooks
**Tipo**: Plataforma de contabilidad y gestión de inventario empresarial

**Protocolo**: REST API / HTTPS

**Función**: Sincroniza datos de inventario entre VineVault y QuickBooks, exporta niveles de stock e integra información contable.

**Patrón de integración**: Bidireccional con sincronización programada o disparada por eventos clave

#### Odoo
**Tipo**: Sistema ERP y gestión de inventario

**Protocolo**: REST API / HTTPS

**Función**: Intercambia datos de inventario entre plataformas y sincroniza catálogos de productos.

**Patrón de integración**: Bidireccional con sincronización programada o disparada por eventos clave

#### Zoho Inventory
**Tipo**: Plataforma de gestión de inventario para PYMES

**Protocolo**: REST API / HTTPS

**Función**: Comparte actualizaciones de inventario en tiempo real y exporta registros detallados de botellas.

**Patrón de integración**: Bidireccional con sincronización programada o disparada por eventos clave

#### Sistema de Soporte

##### Ticketing System
**Tipo**: Plataforma externa de gestión de tickets de soporte

**Ejemplos de proveedores**: Zendesk, Freshdesk, Jira Service Management

**Protocolo**: HTTPS / Widget API

**Función**: Plataforma centralizada que recibe, gestiona y rastrea tickets de soporte creados por usuarios de VineVault.

**Acceso de usuarios**: Widget embebido directamente en la SPA de VineVault permite crear tickets sin salir de la aplicación.

**Flujo de soporte**:
1. Usuario abre widget de soporte embebido en VineVault SPA
2. Usuario crea nuevo ticket con descripción del problema
3. Ticketing System recibe solicitud vía HTTPS/Widget API
4. Ticketing System notifica automáticamente al Support Team
5. Support Team revisa ticket en Ticketing System
6. Support Team resuelve el problema
7. Usuario recibe actualizaciones en VineVault mediante widget

#### Flujos de Comunicación Principales

 **Autenticación**
Usuario → Landing Page → Google OAuth2 → JWT → VineVault →  Sesión iniciada

 **Monitoreo Ambiental**
ESP32 (GPIO/I2C) → MQTT/HTTPS → VineVault → ¿Threshold? → Resend →  Alerta usuario

 **Pagos**
Usuario → Stripe API → Pago → Webhook → VineVault → Resend →  Confirmación

 **IA Recomendaciones**
Datos (inventario/consumo/telemetría) → API Generativa → Insights → VineVault →  Usuario ve recomendaciones

 **Sincronización Inventario**
VineVault ⇄ API (QB/Odoo/Zoho) ⇄ Confirmación →  Estado actualizado

**Tickets Soporte**
Widget SPA → API Ticketing → Ticket + Notif → Soporte → Resolución →  Usuario rastrea


#### Límites del Sistema VineVault

##### Dentro de VineVault (Responsabilidad VineVault)
- Autenticación y autorización de usuarios (con delegación a Google)
- Gestión de suscripciones y facturación (orquestación con Stripe)
- Catálogo de vinos e inventario de botellas
- Monitoreo ambiental y detección de anomalías
- Análisis e insights de inventario (con IA)
- Gestión centralizada de notificaciones
- Coordinación de integraciones y exportaciones

##### Fuera de VineVault (Responsabilidad de terceros)
- Verificación de identidad (Google OAuth2)
- Procesamiento de pagos real (Stripe)
- Almacenamiento seguro de contraseñas de terceros
- Hardware físico de sensores (ESP32)
- Algoritmos de inteligencia artificial avanzada (proveedores IA)
- Gestión de tickets de soporte (plataforma especializada)
- Operaciones contables y ERP (sistemas empresariales)
- Entrega de emails (Resend)

#### Principios de Comunicación

**Seguridad por defecto**: Todas las comunicaciones externas utilizan HTTPS/TLS 1.3. Las credenciales sensibles nunca se almacenan directamente en VineVault.

**Desacoplamiento**: Las integraciones con terceros se realizan mediante APIs REST y webhooks, minimizando dependencias críticas. Si un sistema externo falla temporalmente, VineVault continúa operativo.

**Eventos asincronos**: Cambios importantes (pagos, tickets, alertas) se transmiten vía webhooks para no bloquear operaciones del usuario.

**Sincronización inteligente**: Los datos críticos se sincronizan de forma asincrónica, permitiendo que el usuario continúe trabajando sin esperas.

**Tolerancia a fallos**: Los componentes clave tienen reintentos automáticos y caché local (ESP32) si falla la conexión.

### 4.3.3. Software Architecture Container Level Diagrams.

<a href="https://ibb.co/b5CfcZVZ"><img src="https://i.ibb.co/TM7C9SGS/Vine-Vault-Containers-dark.png" alt="Vine-Vault-Containers-dark" border="0"></a>


#### Descripción General

El diagrama de contenedores de VineVault muestra la estructura interna de la plataforma y cómo cada componente trabaja de forma independiente pero conectada. La arquitectura está dividida en frontend, backend, base de datos, dispositivos IoT e integraciones externas.

#### Contenedores de Presentación

##### Landing Page
- Sitio web público desarrollado con HTML, CSS y JavaScript.
- Presenta información de VineVault y permite acceder al login.
- Optimizado para SEO y diseño responsive.

##### Web App
- Aplicación en Vue 3 encargada de la autenticación.
- Gestiona sesiones seguras con Google OAuth2 y JWT.
- Carga la SPA principal tras validar al usuario.

##### SPA (Single Page Application)
- Interfaz interactiva desarrollada en Vue 3.
- Permite monitorear inventario, sensores, reportes y recomendaciones IA.
- Se comunica con el backend mediante API Gateway.
- Incluye dashboards, gráficos y soporte integrado.

#### Contenedores Backend

##### API Gateway
- Punto de entrada único del sistema.
- Maneja seguridad, routing, rate limiting y validación de solicitudes.
- Recibe tráfico desde SPA, Stripe y dispositivos IoT.

##### Platform API
- Núcleo de la lógica de negocio desarrollado en Spring Boot.
- Gestiona autenticación, inventario, facturación, monitoreo ambiental, notificaciones e integraciones.
- Orquesta la comunicación con PostgreSQL y servicios externos.

##### PostgreSQL Database
- Base de datos relacional principal.
- Almacena usuarios, vinos, sensores, facturación, telemetría y auditorías.
- Soporta transacciones ACID, backups y alta disponibilidad.

#### Contenedor IoT

##### ESP32 Sensor Device
- Dispositivo físico que captura temperatura y humedad de la cava.
- Envía telemetría mediante MQTT/HTTPS.
- Tiene caché local y sincronización automática si falla la conexión.

##### Sistemas Externos

VineVault se integra con:
- Google OAuth2 (autenticación)
- Stripe (pagos)
- Resend (emails)
- Servicios de IA generativa
- QuickBooks, Odoo y Zoho Inventory

#### Flujos Principales

##### Flujo de Aplicación
Usuario → SPA → API Gateway → Platform API → PostgreSQL

#### Flujo IoT
ESP32 → API Gateway → Platform API → PostgreSQL → Alertas

##### Flujo de Pagos
SPA → Stripe → Webhook → Platform API → PostgreSQL

#### Flujo de IA
Platform API → Servicio IA → Recomendaciones → SPA

#### Infraestructura

##### Escalabilidad
- Backend escalable horizontalmente con múltiples instancias.
- CDN para frontend.
- PostgreSQL optimizado con réplicas.

##### Seguridad
- TLS 1.3
- OAuth2 y JWT
- RBAC y auditoría
- Encriptación AES-256

##### Monitoreo
- Logs centralizados
- Prometheus + Grafana
- Alertas automáticas y trazabilidad distribuida


### 4.3.4. Software Architecture Deployment Diagrams.

<a href="https://ibb.co/Q78pyWpy"><img src="https://i.ibb.co/KcNbTtbT/Production-dark-1.png" alt="Production-dark-1" border="0"></a>


####  Resumen General
La plataforma VineVault es un ecosistema de software e IoT diseñado para la gestión integral, monitoreo de condiciones críticas (temperatura y humedad) y optimización inteligente de bodegas de vino de alta gama. 


####  Vista de Despliegue: Desglose por Capas e Infraestructura

El diseño adopta una arquitectura de sistemas distribuidos, estructurada bajo el patrón de **Capas Lógicas Desacopladas (N-Tier Architecture)**, garantizando que el fallo de un componente no comprometa la disponibilidad total del ecosistema.

##### Capa de Presentación y Distribución (Web Hosting)
Orientada a optimizar la experiencia de usuario (UX), el tiempo de carga y el SEO.
* **Landing Page:** Nodo estático optimizado para el tráfico público e indexación de motores de búsqueda. Implementa una redirección segura (HTTPS) hacia la aplicación web central al iniciar sesión.
* **Web App:** Servidor de distribución encargado exclusivamente de servir los artefactos del cliente web.
* **Single Page Application (SPA):** Ejecutada del lado del navegador del cliente (*Client-side execution*). Descarga la lógica de renderizado del servidor, interactuando de forma completamente asíncrona con el backend mediante peticiones HTTPS REST/GraphQL a través del API Gateway.

#####  Capa de Ingestión y Periferia IoT (ESP32 Device Layer)
El hardware físico es un pilar crítico para la captura de telemetría en tiempo real.
* **ESP32 Hardware (Dispositivo Físico):** Sensor físico de temperatura y humedad de alta precisión instalado directamente en las bodegas de vino.
* **ESP32 Sensor Device (Firmware):** Microcontrolador que ejecuta software embebido encargado de leer periódicamente las métricas ambientales, aplicar filtros de ruido en los datos y transmitir la telemetría cifrada hacia la nube de VineVault de manera persistente o por eventos parametrizados.

#### Núcleo del Sistema y Orquestación (VineVault Cloud)
Aislado dentro de una red privada virtual (VPC) para mitigar vectores de ataque directos.

1.  **Gateway Container (API Gateway):**
    * *Justificación:* Actúa como el único punto de entrada (*Reverse Proxy*) para todo el tráfico externo (tanto de la SPA como de los dispositivos IoT).
    * *Funcionalidades:* Enrutamiento dinámico de peticiones (`Route Requests`), terminación de TLS/SSL, abstracción de microservicios, y enmascaramiento de la topología interna del backend. Protege al núcleo de ataques distribuidos (DDoS) mediante políticas de *Rate Limiting*.
2.  **Java Virtual Machine (Platform API Container):**
    * *Justificación:* Se seleccionó la plataforma JVM por su robustez en entornos empresariales, excelente manejo de concurrencia multi-hilo (esencial para la ingesta simultánea de miles de sensores IoT) y madurez de su ecosistema de seguridad.
    * *Responsabilidades:* Orquestación de la lógica de negocio, procesamiento de telemetría entrante, validación de reglas de inventario, cálculo de alertas por desviaciones térmicas y coordinación con servicios externos.
3.  **Database Server Container (PostgreSQL Database):**
    * *Justificación:* Sistema de gestión de bases de datos relacionales (RDBMS) elegido por su estricto cumplimiento de las propiedades ACID, asegurando la consistencia transaccional del inventario de vinos y los movimientos de stock.
    * *Estructura de Datos:* Almacena información de usuarios, histórico denso de telemetría de sensores, movimientos de inventario, umbrales de alerta física, suscripciones de pago y logs operativos.



####  Estrategia de Integración de Servicios Externos (SaaS)

Para mantener el principio de **Responsabilidad Única (Single Responsibility Principle)** y acelerar el *Time-to-Market*, se delegaron las capacidades genéricas del sistema a proveedores líderes en el mercado a través de integraciones seguras desde la *Platform API*:

| Servicio Externo | Tipo de Componente | Propósito y Justificación Arquitectónica |
| :--- | :--- | :--- |
| **Google OAuth2** | Identidad (IdP) | Autenticación remota y social login seguro. Evita almacenar credenciales sensibles en la base de datos local, reduciendo el riesgo normativo y elevando la seguridad. |
| **Resend** | Notificaciones (Mailing) | Motor de entrega de correos electrónicos transaccionales de alta disponibilidad. Utilizado para notificaciones críticas e inmediatas de alertas térmicas y reportes automatizados. |
| **Stripe** | Pasarela de Pagos | Procesamiento de checkout y gestión de suscripciones de los clientes. Cumple con la normativa PCI-DSS de manera nativa, aislando a VineVault de la manipulación directa de datos financieros. Envía confirmaciones asíncronas vía *Webhooks*. |
| **Generative AI Service** | Inteligencia Artificial | Conexión con LLMs de última generación (Gemini, GPT, Claude). Orquesta datos analíticos del inventario y telemetría para generar layouts inteligentes de bodegas, predicciones de maduración y reportes analíticos en lenguaje natural. |


####  Flujos Críticos de Información

1.  **Flujo de Telemetría:** `ESP32 Sensor Device` $\rightarrow$ `API Gateway` $\rightarrow$ `Platform API (JVM)` $\rightarrow$ Escritura en `PostgreSQL Database`. Si se detecta una anomalía, la API dispara un evento asíncrono a `Resend` para alertar al sommelier/administrador.
2.  **Flujo de Consulta Inteligente (AI):** `SPA Cliente` $\rightarrow$ `Gateway` $\rightarrow$ `Platform API`. La API extrae métricas históricas de `PostgreSQL`, estructura un *prompt* enriquecido con contexto del negocio y lo envía al `Generative AI Service`, devolviendo recomendaciones de conservación personalizadas a la interfaz de usuario en segundos.
