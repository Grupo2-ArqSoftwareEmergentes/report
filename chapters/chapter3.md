# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping.

**To-Be Scenario Mapping Segmento 1:**
<br /><img src="../assets/images/to_be_segmento1.jpg" alt="to_be_segmento1.jpg" width="500">

**To-Be Scenario Mapping Segmento 2:**
<br /><img src="../assets/images/to_be_segmento2.jpg" alt="to_be_segmento1.jpg" width="500">


## 3.2. User Stories.

La presente sección detalla las Historias de Usuario que guiarán el desarrollo de la plataforma VineVault.

| Story ID | Título | Descripción | Criterios de Aceptación | Epic ID |
| --- | --- | --- | --- | --- |
| **US01** | Register a new account | **Como** usuario nuevo, **quiero** registrar una cuenta con mis datos personales **para** acceder a las funciones de gestión de mi cava. | 1. El sistema debe validar que el correo no esté registrado previamente.<br>2. La contraseña debe tener al menos 8 caracteres y un símbolo.<br>3. Enviar correo de confirmación al finalizar. | EP01 |
| **US02** | Select User Profile | **Como** usuario registrado, **quiero** elegir entre un perfil comercial o privado **para** que la interfaz se adapte a mi tipo de uso (Restaurante o Coleccionista). | 1. El usuario debe poder cambiar el perfil en la configuración inicial.<br>2. La interfaz debe mostrar métricas de "Venta" para negocios y "Consumo" para coleccionistas. | EP01 |
| **US03** | Register a new bottle | **Como** usuario, **quiero** registrar una etiqueta con su añada y tipo de vino **para** mantener mi inventario digital actualizado. | 1. Permitir el ingreso manual de bodega, cepa y año.<br>2. El sistema debe permitir asignar una ubicación específica (estante/fila).<br>3. Mostrar mensaje de éxito tras el registro. | EP02 |
| **---** | **---** | **---** | **---** | **---** |
| **US04** | Search and filter stock | **Como** sommelier o coleccionista, **quiero** filtrar mis vinos por tipo o precio **para** encontrar rápidamente la botella que necesito. | 1. Incluir barra de búsqueda por nombre de etiqueta.<br>2. Filtros por categoría: Tinto, Blanco, Espumante, Rosado.<br>3. Filtro por rango de añadas. | EP02 |
| **US05** | Register uncorking | **Como** usuario, **quiero** marcar una botella como "descorchada" **para** que se reste automáticamente del stock disponible. | 1. El usuario debe confirmar la acción antes de procesar.<br>2. El sistema debe registrar la fecha y hora de la salida del stock. | EP02 |
| **US06** | Pair IoT Sensor | **Como** administrador de la cava, **quiero** vincular el sensor de temperatura mediante Wi-Fi **para** recibir datos ambientales en la app. | 1. El proceso de vinculación no debe exceder los 3 pasos.<br>2. Mostrar estado de conexión "En línea/Fuera de línea" en tiempo real. | EP03 |
| **---** | **---** | **---** | **---** | **---** |
| **US07** | Real-time Dashboard | **Como** usuario, **quiero** ver indicadores visuales de temperatura y humedad **para** asegurar que mis vinos no sufran degradación térmica. | 1. Actualización de datos cada 5 minutos como mínimo.<br>2. Uso de colores: Verde (Óptimo), Amarillo (Precaución), Rojo (Crítico). | EP03 |
| **US08** | Set Thermal Alerts | **Como** dueño de la cava, **quiero** configurar umbrales máximos de temperatura **para** recibir una notificación push si hay una falla climática. | 1. Permitir al usuario definir el límite (ej. 18°C).<br>2. La notificación debe llegar en menos de 10 segundos tras detectarse el exceso. | EP03 |
| **US09** | Monthly Rotation Report | **Como** dueño de negocio, **quiero** recibir un reporte de botellas estancadas **para** crear promociones y evitar que el capital se pierda. | 1. El reporte debe listar botellas con más de 60 días sin movimiento.<br>2. Opción de exportar el reporte en formato PDF. | EP04 |
| **US10** | Thermal Traceability | **Como** coleccionista, **quiero** ver el historial climático de una botella específica **para** garantizar su calidad al momento de una venta o descorche. | 1. Mostrar gráfico histórico de temperatura desde que la botella ingresó.<br>2. Indicar el porcentaje de tiempo que la botella estuvo en rango ideal. | EP04 |


## 3.3. Impact Mapping.

El **Impact Mapping** constituye una técnica de planeación estratégica que nos ayuda a visualizar la relación entre las metas del negocio y la entrega de valor a los actores clave.
<br /><img src="../assets/images/impact_mapping.png" alt="impact_mapping.png" width="500">

    
## 3.4. Product Backlog.

El Product Backlog constituye el inventario centralizado y priorizado de todos los requisitos, funcionalidades y mejoras necesarias para la materialización de la solución 

URL del backlog en Jira: https://goo.su/



<img src="https://i.imgur.com/.png" alt="backlog1" width="1000">


| N    | Epic / Story ID | Título | Descripción | Story Points |
| ---- | --- | --- | --- | --- |
| 1    | .            | .                    | . | 2            |
