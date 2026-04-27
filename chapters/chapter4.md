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
#### 4.1.2.1. Quality attribute Scenarios.
#### 4.1.2.1. Constraints.

### 4.1.3. Architectural Drivers Backlog.
### 4.1.4. Architectural Design Decisions.
### 4.1.5. Quality Attribute Scenario Refinements.

## 4.2. Strategic-Level Domain-Driven Design.

### 4.2.1. EventStorming.

Step 1: Unstructured Exploration
<td> <img src="../assets/eventstorming/step1.jpg" alt="Step1"></td>
Step 2: Timelines
<td> <img src="../assets/eventstorming/step2.jpg" alt="Step2"></td>
Step 3: Paint Points
<td> <img src="../assets/eventstorming/step3.jpg" alt="Step3"></td>
Step 4: Pivotal Points
<td> <img src="../assets/eventstorming/step4.jpg" alt="Step4"></td>
Step 5: Commands
<td> <img src="../assets/eventstorming/step5.jpg" alt="Step5"></td>
Step 6: Policies
<td> <img src="../assets/eventstorming/step6.jpg" alt="Step6"></td>
Step7: ReadModels
<td> <img src="../assets/eventstorming/step7.jpg" alt="Step7"></td>
Step 8: External Systems
<td> <img src="../assets/eventstorming/step8.jpg" alt="Step8"></td>
Step 9: Aggregates
<td> <img src="../assets/eventstorming/step9.jpg" alt="Step9"></td>

### 4.2.2. Candidate Context Discovery.

<td> <img src="../assets/candidatecontext/candidate.jpg" alt="Step9"></td>

### 4.2.3. Domain Message Flows Modeling.

<td> <img src="../assets/dmfm/scenario1.jpg" alt="Scenario1"></td>

<td> <img src="../assets/dmfm/scenario2.jpg" alt="Scenario2"></td>

<td> <img src="../assets/dmfm/scenario3.jpg" alt="Scenario3"></td>

<td> <img src="../assets/dmfm/scenario4.jpg" alt="Scenario4"></td>

### 4.2.4. Bounded Context Canvases.
En esta sección el equipo diseña sus candidate bounded contexts, detallando los 
criterios de diseño. El equipo debe ir seleccionando cada bounded context, por 
orden de importancia, para elaborar su Bounded Context Canvas. La elaboración del 
Bounded Context Canvas debe seguir un proceso iterativo con los pasos de Context 
Overview Definition, Business Rules Distillation & Ubiquitous Language Capture, 
Capability Analysis, Capability Layering (si aplica), Dependencies Capture, y Design 
Critique.

### 4.2.5. Context Mapping.
En esta sección el equipo explica y evidencia el proceso de elaboración de un 
conjunto de contexts maps (visualizaciones de las relaciones estructurales entre 
bounded contexts). Para ello el equipo revisa información recolectada y la utiliza 
para producir los diseños candidatos. Se recomienda en el proceso incluir preguntas 
como: “¿qué pasaría si movemos este capability a otro bounded context?”, “¿qué 
pasaría si descomponemos este capability y movemos uno de los sub-capabilities a 
otro bounded context?”, “¿qué pasaría si partimos el bounded context en múltiples 
bounded contexts?”, “¿qué pasaría si tomamos este capability de estos 3 contexts y 
lo usamos para formar un nuevo context?”, “¿qué pasaría si duplicamos una 
funcionalidad para romper la dependencia?”, “¿qué pasaría si creamos un shared
service para reducir la duplicación entre múltiples bounded contexts?”, “¿qué 
pasaría si aislamos los core capabilities y movemos los otros a un context aparte?”. 
Debe finalizar este proceso discutiendo cada alternativa de context mapping a fin de 
llegar a la mejor aproximación. Es importante que el equipo considere los patrones 
de relaciones entre Bounded Contexts establecidos en Domain-Driven Design, como 
Anti-corruption Layer, Conformist, Customer/Supplier ó Shared Kernel

## 4.3. Software Architecture.

### 4.3.1. Software Architecture System Landscape Diagram.
### 4.3.2. Software Architecture Context Level Diagrams.
### 4.3.3. Software Architecture Container Level Diagrams.
### 4.3.4. Software Architecture Deployment Diagrams.
