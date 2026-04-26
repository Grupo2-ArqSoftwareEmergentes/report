# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Attribute-Driven Design.

### 4.1.1. Design Purpose.
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
En esta sección, el equipo explica y evidencia el proceso seguido para visualizar cómo 
deben colaborar los bounded contexts para resolver los casos que se presentan en el 
negocio para los usuarios del sistema. Para ello debe aplicar la técnica de 
visualización Domain Storytelling. Complemente la explicación con capturas en 
imágenes de los diagramas de Domain Storytelling elaborados.

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