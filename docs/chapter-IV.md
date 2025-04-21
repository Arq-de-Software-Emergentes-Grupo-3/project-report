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

### 4.2.2. Candidate Context Discovery

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

### 4.2.3. Domain Message Flows Modeling

Los Domain Message Flows modelan las interacciones entre los diferentes bounded contexts, mostrando cómo se comunican entre sí mediante comandos, eventos y consultas. A continuación, presentamos los flujos de mensaje para cuatro escenarios clave de nuestra aplicación:

**Scenario 1: Access platform as a new user**

Este flujo de mensajes modela cómo un usuario nuevo accede a la plataforma WasteTrack, ilustrando las interacciones entre el usuario y el bounded context de Access, y cómo este se comunica con el contexto de Monitoring.

<img src="../assets/img/chapter-IV/messageFlow1.jpg"> 

Este flujo demuestra la relación Customer-Supplier entre Access y Monitoring, donde Access actúa como proveedor de información de autenticación y autorización.

**Scenario 2: Select favorite container**

Este flujo modela cómo un usuario selecciona un contenedor como favorito para recibir notificaciones específicas sobre su estado.

<img src="../assets/img/chapter-IV/messageFlow2.jpg"> 

Este flujo ilustra cómo la interacción del usuario con el sistema desencadena cambios en múltiples bounded contexts utilizando el patrón de comunicación basado en eventos.

**Scenario 3: Generating route simulation**

Este flujo muestra el proceso de generación de una simulación de ruta optimizada para la recolección de residuos.

<img src="../assets/img/chapter-IV/messageFlow3.jpg"> 

Este flujo demuestra la relación Partnership entre Simulation y Monitoring, así como la relación Customer-Supplier entre IoT Device y Simulation.

**Scenario 4: Alert user when favorite container overflow**

Este flujo ilustra cómo el sistema detecta y notifica a un usuario cuando su contenedor favorito está por desbordarse.

<img src="../assets/img/chapter-IV/messageFlow4.jpg"> 

Este flujo demuestra cómo se implementa el patrón Published Language entre IoT Device y Monitoring, permitiendo una comunicación estandarizada sobre el estado de los contenedores que beneficia directamente a los usuarios finales.

Estos flujos de mensaje son fundamentales para entender cómo los diferentes componentes de nuestro sistema interactúan entre sí, permitiéndonos identificar posibles cuellos de botella, optimizar la comunicación y garantizar que la arquitectura responda adecuadamente a los casos de uso principales.

### 4.2.4. Bounded Context Canvases

Los Bounded Context Canvases son herramientas visuales que nos permiten documentar las características fundamentales de cada contexto delimitado, capturando su propósito estratégico, modelo de dominio, lenguaje ubicuo, políticas y relaciones con otros contextos. A continuación, presentamos los canvases para nuestros cuatro bounded contexts identificados, que nos ayudaron a definir claramente las responsabilidades y límites de cada uno.

**Access Bounded Context:** Este canvas detalla nuestro contexto de acceso, responsable de la autenticación y autorización. Definimos sus principales modelos de dominio (Usuario, Rol, Permiso), las políticas de seguridad y los eventos clave como el registro de usuario y la autenticación. Su propósito estratégico es garantizar que solo los usuarios autorizados puedan acceder a funcionalidades específicas del sistema, actuando como proveedor upstream para otros contextos. El canvas ilustra claramente cómo este contexto encapsula toda la lógica relacionada con la identidad y seguridad.

<img src="../assets/img/chapter-IV/boundedContext3.jpg">

**Monitoring Bounded Context:** Este canvas muestra nuestro contexto de monitoreo, que representa el núcleo de la experiencia del usuario con la aplicación. Identificamos sus principales entidades (Contenedor, Favorito, Alerta) y las capacidades clave como visualización de contenedores en tiempo real, sistema de favoritos y notificaciones. Este contexto actúa como cliente downstream de Access e IoT Device, mientras mantiene una relación de partnership con Simulation. El canvas nos permitió visualizar la complejidad de este contexto y sus múltiples integraciones.

<img src="../assets/img/chapter-IV/boundedContext1.jpg">

**Simulation Bounded Context:** El canvas de simulación refleja la sofisticación técnica de este contexto, mostrando su responsabilidad en la optimización de rutas y predicciones. Documentamos sus modelos de dominio principales (Ruta, Simulación, Parámetro), sus algoritmos de optimización y su dependencia de los datos históricos proporcionados por IoT Device. Este contexto implementa un ACL para transformar los datos del IoT en formatos adecuados para sus algoritmos de optimización, lo que se refleja claramente en el canvas.

<img src="../assets/img/chapter-IV/boundedContext4.jpg">

**IoT Device Bounded Context:** Este canvas presenta nuestro contexto más cercano al hardware, responsable de gestionar los dispositivos físicos y sus sensores. Identificamos sus principales agregados (Dispositivo, Sensor, Medición), los eventos que genera (como cambios en el nivel de llenado) y su rol como publicador de datos para otros contextos. El canvas muestra claramente cómo este contexto implementa un patrón Published Language para estandarizar la comunicación con Monitoring y Simulation.

<img src="../assets/img/chapter-IV/boundedContext2.jpg">

Estos canvases fueron herramientas fundamentales para definir la arquitectura de nuestra solución, permitiéndonos visualizar cada contexto como una unidad coherente con responsabilidades claras y bien definidas. Además, nos ayudaron a identificar los puntos de integración entre contextos que luego refinamos en el Context Mapping.

### 4.2.5. Context Mapping

Después de identificar nuestros bounded contexts (Access, Monitoring, Simulation e IoT Device), procedimos a definir las relaciones entre ellos mediante la técnica de Context Mapping. Este proceso nos permitió visualizar cómo estos contextos se comunican y colaboran entre sí en nuestro sistema WasteTrack.

**Proceso de elaboración**
Para elaborar nuestro Context Map, analizamos varias alternativas evaluando diferentes escenarios y relaciones posibles entre los bounded contexts:

- Alternativa 1: Modelo Inicial

<img src="../assets/img/chapter-IV/contextMapping1.png"> 

Donde: U/D: Upstream/Downstream (relación Cliente/Proveedor)

En este modelo inicial, Access actúa como proveedor para Monitoring, proporcionando autenticación de usuarios. IoT Device suministra datos a Simulation y Monitoring para el seguimiento y optimización de rutas.

- Alternativa 2: Con Anti-corruption Layer

Consideramos la inclusión de Anti-corruption Layers para proteger los modelos de dominio:

<img src="../assets/img/chapter-IV/contextMapping2.png"> 

Donde: ACL: Anti-corruption Layer

Esta alternativa añade capas de traducción para proteger los modelos de dominio cuando la comunicación cruzaba fronteras de contexto.

- Alternativa 3: Con Shared Kernel

Evaluamos si algunas funcionalidades compartidas podrían beneficiarse de un Shared Kernel:

<img src="../assets/img/chapter-IV/contextMapping3.png"> 

En esta alternativa, IoT Device y Simulation comparten un kernel común para el modelo de estado de los contenedores.

**Evaluación de alternativas**
Nos planteamos las siguientes preguntas clave para evaluar nuestras alternativas:

1. ¿Qué pasaría si movemos la gestión de alertas del IoT Device al contexto de Monitoring?

- Ventaja: Simplificaría la interfaz para el usuario final
- Desventaja: Crearía una fuerte dependencia y acoplamientos indeseados

2. ¿Qué pasaría si descomponemos el capability de optimización de rutas en Simulation y movemos parte a un nuevo contexto?

- Ventaja: Mejor separación de responsabilidades
- Desventaja: Aumentaría la complejidad de coordinación entre contextos

3. ¿Qué pasaría si duplicamos la funcionalidad de consulta de estado en IoT Device y Monitoring para romper dependencias?

- Ventaja: Mayor autonomía entre contextos
- Desventaja: Posible inconsistencia de datos y mayor mantenimiento

4. ¿Qué pasaría si creamos un shared service para gestionar notificaciones entre múltiples bounded contexts?

- Ventaja: Evita duplicación de código y unifica la experiencia de notificaciones
- Desventaja: Introduce una dependencia compartida que podría limitar la evolución independiente

**Modelo de Context Map Final**

Después de evaluar todas las alternativas, optamos por el siguiente Context Map:

<img src="../assets/img/chapter-IV/contextMapping4.png"> 

**Relaciones entre contextos:**

1. Access ↔ Monitoring (Customer-Supplier):

- Access actúa como proveedor (Upstream) proporcionando autenticación y autorización
- Monitoring actúa como cliente (Downstream) consumiendo la información de usuarios autenticados
- Se implementa un Anti-corruption Layer en Monitoring para traducir el modelo de usuario de Access

2. IoT Device ↔ Monitoring (Published Language):

- IoT Device publica datos de sensores en un formato estandarizado
- Monitoring se suscribe a estos datos para mostrar información en tiempo real
- Ambos contextos acuerdan un lenguaje común para la comunicación

3. IoT Device ↔ Simulation (Customer-Supplier):

- IoT Device proporciona datos históricos y en tiempo real (Upstream)
- Simulation consume estos datos para generar predicciones y optimizar rutas (Downstream)
- Simulation implementa un Anti-corruption Layer para transformar los datos del IoT

4. Simulation ↔ Monitoring (Partnership):

- Ambos contextos colaboran estrechamente para proporcionar una experiencia completa
- Comparten algunos modelos y conceptos, pero mantienen su independencia
- La comunicación es bidireccional y fluida

**Justificación:**

Elegimos este modelo porque:

1. Mantiene una clara separación de responsabilidades entre contextos
2. Usa Anti-corruption Layers donde es necesario proteger los modelos de dominio
3. Establece un Published Language para estandarizar la comunicación entre IoT Device y otros contextos
4. Crea una Partnership entre Simulation y Monitoring que refleja su estrecha colaboración
5. Evita la creación de dependencias innecesarias que dificultarían la evolución del sistema
6. Permite que cada equipo trabaje con autonomía en su bounded context

Este Context Map proporciona una base sólida para el desarrollo de nuestro sistema WasteTrack, facilitando la comunicación entre equipos y estableciendo claramente las interacciones entre los diferentes dominios de la aplicación.

### 4.3. Software Architecture

#### 4.3.1. Software Architecture System Landscape Diagram

#### 4.3.2. Software Architecture Context Level Diagrams

#### 4.3.3. Software Architecture Container Level Diagrams

#### 4.3.4. Software Architecture Deployment Diagrams
