# Capítulo I: Introducción

## 1.1. Startup Profile

### 1.1.1. Descripción de la Startup

**VineVault** es una plataforma integral diseñada para digitalizar la gestión de cavas y bodegas, unificando el control de inventario con el monitoreo ambiental en tiempo real. Basada en una arquitectura de monitoreo inteligente, la solución está pensada para resolver los dos problemas principales del sector en Latinoamérica: la falta de visibilidad del stock y el riesgo de pérdida de producto por condiciones climáticas inadecuadas.

- **Misión:** 

Transformar la pasión y el negocio del vino en una experiencia digital sin complicaciones. Ayudamos a restaurantes y coleccionistas a proteger su inversión y gestionar su inventario de forma ágil, eliminando errores manuales y garantizando la calidad de cada botella mediante tecnología accesible.

- **Visión:** 

Convertirnos en el estándar tecnológico para la gestión de bebidas premium en Latinoamérica, siendo reconocidos como la herramienta que mejor entiende el equilibrio entre la tradición del vino y la precisión de la tecnología moderna.

### 1.1.2. Perfiles de integrantes del equipo

| Foto del estudiante | Nombres y apellidos | Código de estudiante | Descripcion |
|---|---|---|---|
| <img src="../assets/members/U202121325.jpg" alt="Ian Macavilca Quispe" width="100"> | Macavilca Quispe, Ian | U202121325 | Soy un estudiante de 21 años, con interes en optimización y diseño de Apps Web/Mobile. Me gusta resolver problemas con ideas creativas. |
| <img src="../assets/members/U201824550.jpg" alt="Javier Kenyi Mendoza Solis" width="100"> | Mendoza Solis, Javier Kenyi | U201824550 | Soy estudiante de quinto ciclo de Ingeniería de Software. Destaco en razonamiento numérico y creativo, con conocimientos en SQL, C++ y Python. Me considero amable, empático y enfocado en generar confianza para un buen trabajo en equipo. |
|<img src="https://camo.githubusercontent.com/240cc4f5cfad98a03626304d463d59fde9918d805e8df2f6ca4ec9970814489d/68747470733a2f2f692e706f7374696d672e63632f476d4a6a513048472f45726e6573746f2d656c6567616e74652e706e67" alt="Javier Kenyi Mendoza Solis" width="100">| Casaverde De La Cruz Ernesto David|U20221B657 |Soy estudiante de Ingeniería de Software, me caracterizo por ser una persona responsable, con escucha activa y enfoque colaborativo. Me comprometo a aportar al trabajo en equipo para lograr resultados de calidad mientras todos aprendemos en el proceso. Además, cuento con conocimientos en programación, incluyendo C++, HTML, CSS y JavaScript.|

## 1.2. Solution Profile

### 1.2.1 Antecedentes y problemática

#### Antecedentes

En el sector de la hospitalidad y el coleccionismo de alta gama, una gestión deficiente de la bodega tiene un costo directo y elevado. Cuando un restaurante o un coleccionista no controla adecuadamente las condiciones de su cava, se enfrenta a riesgos críticos: desde la oxidación de etiquetas costosas por fallas térmicas hasta la pérdida de capital por stock inmovilizado.

- Pérdida por Almacenamiento: Según la FAO, una parte significativa de las mermas en la cadena de bebidas ocurre por fallas en el almacenamiento. En vinos premium, una variación de pocos grados puede arruinar años de maduración, convirtiendo una inversión en una pérdida total.

- Brecha Tecnológica: En Latinoamérica, más del 60% de las pymes del sector servicios (restaurantes y bares) aún dependen de procesos manuales o de hojas de cálculo dispersas para controlar sus existencias. Según Gartner, esta falta de digitalización genera errores humanos constantes y una toma de decisiones reactiva, no proactiva.

- El Problema de la Rotación: El flujo de caja se ve afectado cuando no hay visibilidad sobre el inventario. Las botellas que permanecen en estante más tiempo del debido representan dinero "congelado". Sin una herramienta que alerte sobre la baja rotación, los establecimientos pierden la oportunidad de optimizar sus cartas y maximizar sus ventas.

Históricamente, este sector ha quedado rezagado en la adopción tecnológica, dejando a los dueños de cavas —ya sean de negocios o privadas— "a ciegas" respecto al estado real y la salud de su patrimonio líquido.


#### Problematica

1. **What (Qué):** 
Pérdida de valor y capital debido a la degradación del vino por condiciones ambientales no controladas (temperatura/humedad) y stock inmovilizado por falta de seguimiento. No se sabe con certeza qué botellas deben consumirse pronto y cuáles corren riesgo de dañarse.
2. **Who (Quién):** 
Al dueño del restaurante o sommelier, que pierde margen de ganancia por mermas; y al coleccionista aficionado, que ve arruinada una inversión personal y emocional en su cava.
3. **Where (Dónde):** 
En las cavas, bodegas de servicio y estantes de exhibición, donde el control actual es visual o basado en suposiciones, sin registros técnicos de las condiciones del aire.
4. **When (Cuándo):** 
Cuando al abrir una botella se descubre que el vino está oxidado o "picado" por mala guarda. O cuando en el cierre de mes se detecta que hay cajas de vino que no se vendieron y están ocupando espacio crítico.
5. **Why (Por qué):** 
Por la ausencia de una herramienta accesible que centralice el inventario y el monitoreo climático. La gestión actual depende de la memoria o de registros manuales que no generan alertas proactivas.

6. **How (Cómo):** 
El usuario olvida registrar una salida o entrada; no tiene forma de saber si durante la madrugada hubo un pico de calor en la bodega. La falta de datos impide una rotación inteligente de las etiquetas.
7. **How Much (Cuánto):** Una sola botella de vino premium dañada puede costar entre $50 y $500 USD. En un restaurante, un stock mal gestionado puede representar miles de dólares en inventario "muerto" que no genera flujo de caja.

### 1.2.2 Lean UX Process.

#### 1.2.2.1. Lean UX Problem Statements.

Hoy en día, la mayoría de los restaurantes de gama media-alta y los coleccionistas particulares en Latinoamérica gestionan sus cavas de manera empírica, confiando en registros manuales o en la memoria para controlar su inventario, mientras que el monitoreo de las condiciones ambientales de temperatura y humedad es prácticamente inexistente. Esta falta de control genera pérdidas críticas, tanto por la degradación irreversible del vino debido a fallas térmicas como por el estancamiento de capital en etiquetas que no rotan por falta de seguimiento. Las herramientas actuales no resuelven el problema, pues suelen ser sistemas de gestión genéricos que no consideran la salud del producto o soluciones industriales de monitoreo con costos y complejidad técnica inasumibles para una pyme o un aficionado. VineVault resuelve esta brecha integrando un almacén virtual intuitivo con tecnología IoT accesible, permitiendo que el usuario proteja su inversión mediante alertas climáticas en tiempo real y optimice su stock a través de reportes mensuales de rotación inteligentes. Iniciamos nuestro despliegue en Perú y la región, enfocándonos en dueños de negocios y apasionados del vino que buscan transformar su bodega en un activo estratégico. Mediremos nuestro éxito logrando que ocho de cada diez usuarios eliminen sus mermas por deterioro ambiental y que los establecimientos incrementen la rotación de sus etiquetas estancadas en al menos un 15% durante su primer trimestre de uso.

#### 1.2.2.2. Lean UX Assumptions.

**User Assumptions**

- Nuestros usuarios son dueños de restaurantes, sommeliers y coleccionistas particulares que gestionan bodegas de vinos de valor medio y alto.

- El producto encajará en sus rutinas de supervisión de cava, actualización de cartas de vino y planificación de menús, momentos en los que se revisa la disponibilidad y el estado de las etiquetas.

- Los usuarios valoran su tiempo y la simplicidad, por lo que requieren una herramienta visualmente elegante y fluida que no exija una curva de aprendizaje técnica ni configuraciones complejas de hardware.

- Los dueños y aficionados buscan, por encima de todo, evitar pérdidas económicas por la degradación térmica del vino y reducir el capital inmovilizado en botellas que no rotan.

- Las características más valoradas serán el monitoreo ambiental automático (pasivo), las notificaciones push preventivas y el reporte mensual de inteligencia que les sugiera qué botellas vender o consumir sin necesidad de analizar datos manualmente.

**User Outcome Assumptions**

- Los dueños y coleccionistas monitorearán el estado de su cava de forma remota y precisa, eliminando el riesgo de pérdida por factores ambientales y el desconocimiento de su inventario real.

- Los usuarios optimizarán su capital al recibir sugerencias de consumo y venta, logrando que las botellas con baja rotación se conviertan en ingresos o experiencias en el momento oportuno.

- La gestión de la bodega pasará de ser una tarea manual y reactiva a un proceso inteligente y preventivo, asegurando que cada botella abierta mantenga la calidad esperada por el cliente o el aficionado.

- Los usuarios se sentirán seguros y en total control de su inversión, reduciendo la ansiedad por posibles fallos climáticos en la cava y ganando confianza al tomar decisiones basadas en datos históricos.

**Business Assumptions**
- Creemos que los dueños de restaurantes y coleccionistas necesitan una herramienta que no solo cuente botellas, sino que proteja activamente la salud de su inversión mediante el monitoreo de variables ambientales.

- Pensamos que una solución que integre hardware (IoT) y software superará a los sistemas de inventario genéricos (POS) al ofrecer datos críticos de preservación que los sistemas actuales ignoran.

- Creemos que un modelo de suscripción mensual será aceptado si demostramos que el costo del software es menor al valor de una sola botella premium que se salva de echarse a perder gracias a nuestras alertas.

- Asumimos que la mayor barrera será la percepción de que el inventario manual es "suficiente", lo cual mitigaremos demostrando visualmente los riesgos de las variaciones térmicas y la pérdida de dinero por stock inmovilizado.

- Reconocemos que si el usuario no percibe el reporte mensual de inteligencia como una ventaja estratégica para su flujo de caja o su experiencia personal, el proyecto no logrará la retención necesaria para ser viable.

**Business Outcome Assumptions**

- Reducir las pérdidas por deterioro térmico en un porcentaje medible dentro de los primeros tres meses, gracias a la respuesta inmediata ante las alertas del sensor IoT.

- Optimizar el flujo de caja de los restaurantes al reducir el stock inmovilizado (etiquetas de baja rotación) mediante el uso de la analítica del reporte mensual.

- Aumentar la confianza y la paz mental de los dueños en la gestión de su inversión, reduciendo la necesidad de revisiones físicas constantes de la cava.

- Lograr un crecimiento orgánico mediante alianzas con proveedores de cavas físicas y tiendas de vinos de alta gama, posicionando a VineVault como el complemento tecnológico indispensable para cualquier bodega seria.

**Feature Assumptions**

- Gestión de cava digital con registro ágil de etiquetas y monitoreo persistente de condiciones críticas (temperatura y humedad) mediante sensores IoT.

- Alertas preventivas inteligentes enviadas directamente al móvil cuando las variables ambientales se desvían de los rangos óptimos de preservación del vino.

- Motor de analítica mensual que genera reportes automáticos sobre la salud de la cava y detecta etiquetas de baja rotación para sugerir su venta o consumo estratégico.

-Dashboard de trazabilidad térmica que permite visualizar el historial de estabilidad de la bodega, garantizando que el producto ha mantenido su calidad desde el ingreso hasta el descorche.

- Selector de perfil de usuario que adapta la terminología y las métricas de éxito según se trate de un entorno de negocio o una colección privada.

#### 1.2.2.3. Lean UX Hypothesis Statements.

- Hipótesis 1: Creemos que reduciremos las pérdidas por deterioro térmico si los dueños de restaurantes y coleccionistas actúan de inmediato ante condiciones ambientales adversas mediante alertas en tiempo real de temperatura y humedad vinculadas a sensores IoT.

- Hipótesis 2: Creemos que optimizaremos el flujo de caja y la rentabilidad de la bodega si los usuarios identifican etiquetas estancadas y reciben sugerencias de venta o consumo a través de un reporte mensual de rotación inteligente.

- Hipótesis 3: Creemos que aseguraremos la calidad organoléptica del vino si los sommeliers y aficionados monitorean la estabilidad histórica de su cava mediante un dashboard de trazabilidad climática.

- Hipótesis 4: Creemos que reduciremos el tiempo dedicado a la gestión administrativa si los usuarios registran sus movimientos de stock de forma ágil en una interfaz simplificada y diseñada específicamente para el contexto de una cava.

- Hipótesis 5: Creemos que fortaleceremos la confianza en la toma de decisiones si los dueños visualizan proyecciones de agotamiento de stock basadas en su ritmo de consumo manual, permitiéndoles planificar sus compras con mayor antelación.

- Hipótesis 6: Creemos que incrementaremos la retención de usuarios si la plataforma adapta automáticamente sus métricas y lenguaje visual según el perfil detectado, brindando una experiencia personalizada en una sola aplicación.

#### 1.2.2.4. Lean UX Canvas.

<table border="1" cellpadding="12" cellspacing="0" width="100%">
  <tr>
    <td valign="top" width="33%">
      <strong>Business Problem</strong><br><br>
      Actualmente, muchos restaurantes y coleccionistas gestionan su cava "a ciegas". No saben con certeza si la temperatura de anoche dañó sus vinos ni qué botellas llevan meses (o años) sin moverse, lo que genera una pérdida silenciosa de dinero. El control se lleva en papeles o en la memoria, y solo se dan cuenta de que un vino se malogró cuando ya es tarde y abren la botella. ¿Cómo podríamos crear una herramienta fácil que use sensores y alertas sencillas para que el dueño sepa que sus vinos están seguros y cuáles debería vender o tomar pronto para no perder su inversión?
    </td>
    <td rowspan="2" valign="top" width="34%">
      <strong>Solution ideas</strong><br><br>
      • Inventario digital simplificado con registro de etiquetas, añadas y alertas de stock para saber exactamente qué hay en la cava.<br><br>
      • Monitoreo ambiental de temperatura y humedad con alertas en tiempo real.<br><br>
      • Reporte mensual de rotación inteligente que detecta botellas "olvidadas" y sugiere promocionarlas o consumirlas antes de que pierdan su punto óptimo.<br><br>      
      • Historial de movimientos manuales para rastrear entradas y salidas de botellas.
    </td>
    <td valign="top" width="33%">
      <strong>Business Outcomes</strong><br><br>
      • <strong>Adopción:</strong> ≥40% de los usuarios configuran su primer sensor y registran al menos 10 botellas en su primera semana.<br><br>
      • <strong>Retención:</strong> ≥30% de los usuarios abren la app al menos una vez por semana para revisar la temperatura o actualizar el stock.<br><br>      
      • <strong>Eficiencia:</strong> Reducción del 20% en pérdidas por caducidad o deterioro.<br><br>
      • <strong>Autonomía:</strong> Menos del 15% de usuarios requieren soporte para tareas básicas.
    </td>
  </tr>
  <tr>
    <td valign="top">
      <strong>Users & Customers</strong><br><br>
      • <strong>Dueños de Restaurantes y Sommeliers:</strong> Profesionales del sector gastronómico en Perú y Latinoamérica que manejan cavas de valor medio-alto. Su prioridad es evitar que el vino se arruine por fallas de temperatura y asegurar que las botellas roten para no tener dinero estancado. Valoran herramientas que les den estatus y seguridad técnica sin quitarles tiempo.<br><br>
      • <strong>Coleccionistas Aficionados:</strong> 
      Personas con cavas privadas en casa que consideran sus botellas una inversión o una pasión personal. No son expertos en tecnología, pero quieren la tranquilidad de saber que sus vinos están madurando en condiciones perfectas. Buscan una app elegante que les avise cuándo es el momento ideal para disfrutar una botella especial.
    </td>
    <td valign="top">
      <strong>User Benefits</strong><br><br>
      1. <strong>Protección de la inversión y tranquilidad</strong> — Eliminar el miedo a que una falla en el aire acondicionado o el clima arruine botellas costosas gracias al monitoreo en tiempo real y alertas inmediatas.<br><br>
      2. <strong>Cava eficiente y mayor rentabilidad</strong> — Reducir el dinero "dormido" identificando botellas que llevan demasiado tiempo sin moverse y recibiendo sugerencias para darles salida.<br><br>
      3. <strong>Garantía de calidad al descorchar</strong> — Tener la certeza de que cada vino se ha mantenido en su rango óptimo de temperatura y humedad, asegurando que el sabor y aroma sean los correctos.<br><br>
      4. <strong>Gestión sin esfuerzo</strong> — Sustituir los cuadernos y hojas de Excel por un inventario digital rápido que se actualiza en segundos y trabaja solo mientras el dueño se enfoca en su negocio o hobby.<br><br>
      5. <strong>Decisiones basadas en datos, no en memoria</strong> — Conocer exactamente qué etiquetas son las favoritas y cuáles están en su punto ideal de maduración para planificar compras o cenas especiales con total confianza.
    </td>
  </tr>
  <tr>
    <td valign="top">
      <strong>Hypotheses</strong><br><br>
      • <strong>H1:</strong> Creemos que lograremos que la mitad de los usuarios registren sus botellas si el proceso de añadir una nueva etiqueta toma menos de 30 segundos gracias a un diseño simplificado.<br><br>
      • <strong>H2:</strong> Creemos que evitaremos mermas por calor si los usuarios reciben una notificación push inmediata cuando la temperatura de la cava supera los 20°C por más de una hora.<br><br>
      • <strong>H3:</strong> Creemos que los usuarios consultarán la app semanalmente si incluimos un indicador visual rápido que resuma el estado de salud de su cava en la pantalla de inicio.<br><br>
      • <strong>H4:</strong> Creemos que los dueños de restaurantes optimizarán su stock si el reporte mensual les resalta al menos 3 etiquetas que no han tenido movimiento en los últimos 60 días.<br><br>
      • <strong>H5:</strong> Creemos que eliminaremos el miedo a la tecnología si los coleccionistas logran vincular su sensor IoT a la red Wi-Fi en menos de 3 pasos desde la aplicación.<br><br>
      • <strong>H6:</strong> Creemos que los usuarios valorarán la suscripción si les demostramos que el costo del servicio es menor al precio de una sola botella premium salvada de una degradación térmica.
    </td>
    <td valign="top">
      <strong>What's the most important thing we need to learn first?</strong><br><br>
      • Necesitamos saber si los dueños y coleccionistas realmente actuarán al recibir una alerta en el celular, o si ignorarán la notificación por falta de confianza en el sensor.<br><br>
      • Aprender si el reporte mensual de "botellas estancadas" es un dato que el usuario valora para crear promociones o cenas, o si prefiere seguir decidiendo por intuición.<br><br>
      • Descubrir si un usuario con poca experiencia técnica puede configurar el sensor y la app por su cuenta en menos de 5 minutos o si el proceso le genera frustración.
    </td>
    <td valign="top">
      <strong>What's the least amount of work we need to do to learn the next most important thing?</strong><br><br>
      Ejecutar un experimento mínimo viable:<br><br>
      1. <strong>Landing page</strong> con video demo y oferta de early access para medir interés y willingness-to-pay.<br><br>
      2. <strong>Prueba piloto</strong> con ~3 cavas durante 2 semanas para validar que las alertas generan acción concreta.<br><br>
      3. <strong>Prototipo interactivo</strong> de baja fidelidad para tests moderados con 8–10 usuarios, enfocado en tareas de inventario diario.<br><br>
      Estos pasos requieren bajo costo y entregan la evidencia clave para decidir la inversión en desarrollo completo.
    </td>
  </tr>
</table>

## 1.3. Segmentos objetivo

| Segmento Objetivo #1:  | Restaurantes y Cavas Comerciales   |
| ---- | --- |
| Aspectos demográficos  | Sexo: Indistinto <br />Edad: 30 a 55 años <br />Nivel socioeconómico: Clase media (C) a media alta (B). Pequeños y medianos empresarios con capital propio invertido en el negocio.  |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica:  Lima Metropolitana   |
| Aspectos psicográficos | Personas que ven el vino como una inversión o un activo crítico, no solo como mercancía. Valoran la exclusividad y la perfección técnica. Tienen un alto miedo a que factores externos (calor, humedad) arruinen su capital. Son perfeccionistas y buscan "paz mental" para poder delegar o disfrutar de su cava sin estar presentes físicamente. |
| Aspectos conductuales  | **Necesidad:** Asegurar que sus botellas no se degraden por el clima y que el stock no se estanque.<br />**Uso de herramientas:** Excel básico, cuadernos de registro, WhatsApp para pedidos y, en algunos casos, software genérico de inventario que no se adapta al rubro. No suelen tener personal técnico dedicado.<br />**Respuesta:**   Reaccionan positivamente ante el uso de tecnología invisible (IoT). Se convencen cuando ven gráficas simples de temperatura y reciben alertas que les permiten "salvar" una botella antes de que se eche a perder. |

<br><br>

| Segmento Objetivo #2:  | Coleccionistas y Aficionados |
| ---- | --- |
| Aspectos demográficos  | Sexo:  <br />Edad: 28 a 50 años <br />Nivel socioeconómico: Clase media alta (B) a alta (A). Personas que compran vinos para guardar (estiba) o para ocasiones especiales.  |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica:  Lima Metropolitana   |
| Aspectos psicográficos | Ven su cava como un tesoro personal o una inversión a largo plazo. Les gusta la tecnología que les da estatus y, sobre todo, "paz mental" cuando viajan o están fuera de casa.|
| Aspectos conductuales  | **Necesidad:** Un "seguro de vida" para sus botellas más caras y saber cuándo una etiqueta está lista para ser disfrutada. <br />**Uso de herramientas:** Apps de cata genericas, cuadernos de notas o simplemente memoria visual de su cava.<br />**Respuesta:**   Reaccionan a alertas preventivas y a interfaces elegantes que les permitan presumir u organizar su colección de forma digital. |


