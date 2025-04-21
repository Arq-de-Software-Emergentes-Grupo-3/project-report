# Capítulo IV: Strategic-Level Software Design

## 4.1. Strategic-Level Attribute-Driven Design

### 4.1.1. Design Purpose

### 4.1.2. Attribute-Driven Design Inputs

#### 4.1.2.1. Primary Functionality (Primary User Stories)

#### 4.1.2.2. Quality attribute Scenarios

#### 4.1.2.3. Constraints

### 4.1.3. Architectural Drivers Backlog

### 4.1.4. Architectural Design Decisions

### 4.1.5. Quality Attribute Scenario Refinements

## 4.2. Strategic-Level Domain-Driven Design

Dentro de esta sección se evidencia el proceso que usamos para descomponer nuestro software en bounded contexts. Utilizando las herramientas de EventStorming y Bounded Context Canvas. 

### 4.2.1. EventStorming

Para la elaboración del EventStorming, el equipo se organizó para encontrar una primera aproximación al modelado del dominio de nuestro proyecto. Durante este proceso seguimos una serie de 9 pasos.

**Paso 1: Collect Domain Events**
En este primer paso, identificamos todos los eventos relevantes del dominio que ocurren en nuestro sistema. Estos eventos representan hechos importantes que suceden durante el proceso de negocio y los capturamos con post-its de color naranja.

<img src="../assets/img/chapter-IV/eventStorming1.png"> 

**Paso 2: Timeline**
Organizamos todos los eventos identificados en una línea temporal, colocándolos en orden cronológico para visualizar mejor el flujo del proceso y entender la secuencia natural de acciones en el sistema.

<img src="../assets/img/chapter-IV/eventStorming2.jpg"> 

**Paso 3: Pain and Pivotal points**
Identificamos los puntos problemáticos (pain points) y los momentos clave (pivotal points) en nuestro proceso. Estos representan áreas que requieren atención especial o que son críticas para el funcionamiento del sistema.

<img src="../assets/img/chapter-IV/eventStorming3.jpg"> 

**Paso 4: Commands**
Agregamos los comandos (representados con post-its azules) que desencadenan los eventos. Estos comandos son las acciones que los usuarios o sistemas externos realizan para provocar cambios en el sistema.

<img src="../assets/img/chapter-IV/eventStorming4.jpg"> 

**Paso 5: Policies**
Definimos las políticas o reglas de negocio (con post-its morados) que reaccionan a ciertos eventos y generan nuevos eventos como resultado. Estas políticas automatizan decisiones basadas en eventos previos.

<img src="../assets/img/chapter-IV/eventStorming5.jpg"> 

**Paso 6: Read models**
Identificamos los modelos de lectura o vistas que los usuarios necesitan para tomar decisiones. Estos representan la información que debe estar disponible en determinados puntos del proceso.

<img src="../assets/img/chapter-IV/eventStorming6.jpg"> 

**Paso 7: External System**
Marcamos los sistemas externos (con post-its rosados) que interactúan con nuestra solución. Estos son componentes fuera de nuestro control directo pero que tienen influencia en el proceso.

<img src="../assets/img/chapter-IV/eventStorming7.jpg"> 

**Paso 8: Aggregates**
Agrupamos los comandos y eventos relacionados en unidades lógicas llamadas agregados (representados con post-its amarillos). Cada agregado encapsula un conjunto coherente de funcionalidades.

<img src="../assets/img/chapter-IV/eventStorming8.jpg"> 

**Paso 9: Bounded Context**
Finalmente, identificamos los contextos delimitados o bounded contexts, que son áreas de responsabilidad distintas dentro del sistema. 

<img src="../assets/img/chapter-IV/eventStorming9.jpg"> 

#### 4.2.2. Candidate Context Discovery

A partir del EventStorming realizado en Miro, nuestro equipo llevó a cabo una sesión de Candidate Context Discovery para identificar los bounded contexts de nuestra solución. Utilizamos principalmente la técnica look-for-pivotal-events durante la sesión.

**Proceso de identificación**

Comenzamos revisando el modelo completo que habíamos construido, prestando especial atención a los eventos pivote y agregados identificados.

<img src="../assets/img/chapter-IV/eventStorming3.jpg"> 

Detección de agrupaciones naturales: Identificamos patrones y agrupaciones naturales de comandos, eventos y políticas que trabajaban sobre las mismas entidades o procesos.

<img src="../assets/img/chapter-IV/eventStorming7.jpg"> 

Nos enfocamos en eventos clave como las configuraciones de notificaciones y alertas que marcan claramente transiciones entre diferentes contextos

<img src="../assets/img/chapter-IV/contextDiscovery1.png"> 

Definición de límites: Trazamos fronteras alrededor de los grupos identificados, estableciendo los límites iniciales de nuestros bounded contexts.

<img src="../assets/img/chapter-IV/eventStorming9.jpg">

Nomenclatura y validación: Nombramos cada bounded context identificado según su responsabilidad principal y validamos que tuvieran coherencia interna y límites claros.

<img src="../assets/img/chapter-IV/contextDiscovery2.png"> 

Como resultado de este proceso, identificamos los siguientes bounded contexts para nuestra solución:

- Access: Responsable del acceso a los usuarios al sistema.
- Monitoring: Permite a los usuarios visualizar los contenedores de basura cercanos a su ubicacion, marcar uno como favorito y recibir alertas/notificaciones personalizadas sobre ese contendor, el horario de los camiones recogedores, entre otras funcionalidades.
- Simulation: Gestiona las simulaciones de las rutas optimizadas para el recojo de desechos de los contenedores inteligentes. Predicciones y configuraciones. 
- IoT Device: Responsable de las alertas del dispositivo y configuraciones del dispositivo IoT para los contenedores inteligentes.

Esta identificación nos proporcionó una base sólida para continuar con el modelado más detallado de cada contexto y sus interacciones.

#### 4.2.3. Domain Message Flows Modeling

#### 4.2.4. Bounded Context Canvases

### 4.2.5. Context Mapping

### 4.3. Software Architecture

#### 4.3.1. Software Architecture System Landscape Diagram

#### 4.3.2. Software Architecture Context Level Diagrams

#### 4.3.3. Software Architecture Container Level Diagrams

#### 4.3.4. Software Architecture Deployment Diagrams
