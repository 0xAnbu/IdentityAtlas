# Plataforma OSINT avanzada: investigación de repositorios y prompt maestro de desarrollo

## 1. Objetivo del proyecto

La propuesta es desarrollar una **plataforma OSINT modular, automatizada, extensible y orientada a grafos de conocimiento**, capaz de investigar entidades y descubrir relaciones a partir de múltiples fuentes públicas y autorizadas.

No debería ser simplemente una interfaz que ejecuta SpiderFoot, Maigret y otras herramientas. Su principal valor diferencial será funcionar como un **motor de investigación que descubre información, contrasta evidencias, identifica relaciones y decide qué investigar a continuación**.

### Capacidades principales

| Área | Funcionalidad objetivo | Prioridad |
|---|---|---|
| Investigación | Introducir nombres, usuarios, emails, empresas, dominios, imágenes y otros identificadores permitidos | P0 |
| Recolección | Ejecutar múltiples herramientas y consultar fuentes heterogéneas | P0 |
| Normalización | Transformar resultados diferentes a un modelo común | P0 |
| Evidencias | Registrar procedencia, fechas, fiabilidad y trazabilidad | P0 |
| Correlación | Encontrar coincidencias y relaciones entre entidades | P0 |
| Grafos | Visualizar entidades, atributos y conexiones interactivamente | P0 |
| Resiliencia | Disponer de varias herramientas para una misma función | P0 |
| Observabilidad | Mostrar visualmente qué herramientas funcionan, fallan o no están configuradas | P0 |
| Automatización | Seleccionar investigaciones adicionales a partir de resultados confirmados | P1 |
| Documentos | Extraer texto, metadatos y entidades de documentos | P1 |
| Imágenes | Analizar metadatos, similitudes y procedencia | P1 |
| Machine learning | Entrenar modelos propios con evidencias etiquetadas | P1 |
| Investigación empresarial | Analizar registros mercantiles, infraestructura y relaciones corporativas | P1 |
| Monitorización | Repetir investigaciones y detectar cambios | P2 |
| Inteligencia generativa | Asistir en investigaciones, formular hipótesis y generar informes verificables | P2 |
| Escalabilidad | Procesar investigaciones grandes mediante tareas distribuidas | P2 |

**P0** significa que debe estar en el primer MVP funcional. **P1** amplía las capacidades de investigación y **P2** introduce funcionalidades avanzadas.

El diseño debe contemplar desde el principio todas las categorías descritas en tus requisitos, aunque sus conectores se desarrollen progresivamente.

Las consultas sobre personas deberán estar limitadas a investigaciones legítimas y autorizadas. El sistema no debe convertir coincidencias débiles en identidades confirmadas ni automatizar la agregación invasiva de datos sensibles de terceros.

---

# 2. Repositorios de GitHub seleccionados

He identificado proyectos que cubren tanto la recolección OSINT como la arquitectura de grafos, las evidencias y la experiencia de investigación.

La selección distingue entre **reutilizar una implementación**, **integrar una herramienta** y **tomar un proyecto únicamente como referencia arquitectónica**.

## 2.1. Proyectos más próximos al objetivo final

Estos son especialmente interesantes porque se parecen al producto completo, no solo a un componente aislado.

| Repositorio | Coincidencia con tu proyecto | Qué aprovecharía |
|---|---|---|
| [OpenOSINT](https://github.com/OpenOSINT/OpenOSINT?utm_source=chatgpt.com) | Muy alta | Correlación, procedencia de evidencias, deduplicación y revisión humana |
| [TRACE](https://github.com/denoflore/trace?utm_source=chatgpt.com) | Muy alta | Investigación local, importación de resultados y visualización |
| [FollowTheMoney](https://github.com/opensanctions/followthemoney?utm_source=chatgpt.com) | Muy alta | Modelo de entidades y relaciones |
| [Aleph](https://github.com/alephdata/aleph?utm_source=chatgpt.com) | Alta | Indexación de documentos, búsqueda y análisis de entidades |
| [SpiderFoot](https://github.com/smicallef/spiderfoot?utm_source=chatgpt.com) | Alta | Automatización y arquitectura de módulos de recolección |
| [Forenix OSS](https://github.com/thunderstornX/forenix-oss?utm_source=chatgpt.com) | Alta | Integridad de evidencias, auditoría y gestión de investigaciones |
| [Kipi](https://github.com/assafkip/kipi?utm_source=chatgpt.com) | Alta | Investigación documental asistida y análisis de grafos |

### A. OpenOSINT

**Repositorio:** [OpenOSINT/OpenOSINT](https://github.com/OpenOSINT/OpenOSINT?utm_source=chatgpt.com)

Es uno de los proyectos más relevantes encontrados.

Su módulo de grafos utiliza entidades FollowTheMoney e incorpora procedencia a nivel de afirmación, almacenamiento acumulativo, deduplicación no destructiva y revisión humana. También ofrece herramientas OSINT mediante CLI e interfaces para agentes. [GitHub](https://github.com/OpenOSINT/OpenOSINT/blob/main/docs/graph.md?utm_source=chatgpt.com)

**Reutilizar o estudiar:**
- Modelo de evidencias y procedencia.
- Correlación entre resultados.
- Deduplicación sin pérdida de datos.
- Exportación a formatos interoperables.
- Revisión de coincidencias ambiguas.

**No copiar:**
- La necesidad de utilizar MCP.
- El acoplamiento de la investigación a un agente LLM.
- Una arquitectura que dependa de proveedores externos para funcionar.

### B. TRACE

**Repositorio:** [TRACE](https://github.com/denoflore/trace?utm_source=chatgpt.com)

Plataforma local de investigación que permite importar resultados de SpiderFoot, gestionar entidades, revisar posibles duplicados y exportar grafos a GraphML o STIX 2.1. [GitHub](https://github.com/denoflore/trace?utm_source=chatgpt.com)

**Reutilizar o estudiar:**
- Interfaz orientada a investigaciones.
- Importación de resultados heterogéneos.
- Distinción visual entre relaciones candidatas y confirmadas.
- Gestión de fuentes y observaciones.
- Exportaciones de grafos.

**No copiar:**
- Restricciones de formatos que impidan incorporar fuentes nuevas.
- Dependencias arquitectónicas innecesarias para una aplicación web local.

### C. FollowTheMoney

**Repositorio:** [opensanctions/followthemoney](https://github.com/opensanctions/followthemoney?utm_source=chatgpt.com)

Es un candidato especialmente sólido para evitar inventar desde cero toda la ontología de investigación. Define modelos de entidades y relaciones utilizados en herramientas como OpenSanctions y Aleph. [GitHub](https://github.com/opensanctions/followthemoney?utm_source=chatgpt.com)

**Reutilizar:**
- Ontología de entidades.
- Relaciones entre personas, organizaciones y documentos.
- Validación y serialización.
- Interoperabilidad entre plataformas.

**No copiar:**
- La orientación exclusivamente financiera.
- La suposición de que toda coincidencia implica identidad.

**Decisión recomendada:** utilizar FollowTheMoney como referencia de interoperabilidad y evaluar su incorporación directa antes de desarrollar una ontología completamente nueva.

### D. Aleph

**Repositorio:** [alephdata/aleph](https://github.com/alephdata/aleph?utm_source=chatgpt.com)

Permite indexar documentos y datos estructurados para facilitar su búsqueda e investigación. Admite, entre otros, documentos PDF, Word, HTML y conjuntos de datos tabulares. [GitHub](https://github.com/alephdata/aleph?utm_source=chatgpt.com)

**Reutilizar o estudiar:**
- Ingesta documental.
- Indexación.
- Extracción de entidades.
- Búsqueda transversal entre colecciones.

**No copiar:**
- Toda su infraestructura desde el primer día.
- Componentes complejos que todavía no aporten valor al MVP.

### E. SpiderFoot

**Repositorio:** [smicallef/spiderfoot](https://github.com/smicallef/spiderfoot?utm_source=chatgpt.com)

Herramienta de automatización OSINT y reconocimiento de superficie de ataque, con un ecosistema extenso de módulos. [GitHub](https://github.com/smicallef/spiderfoot/blob/master/README.md?utm_source=chatgpt.com)

**Reutilizar o estudiar:**
- Arquitectura de módulos.
- Clasificación de resultados.
- Encadenamiento de descubrimientos.
- Integración con fuentes heterogéneas.

**No copiar:**
- La lógica de propagación automática sin controles de confianza.
- Todos sus módulos indiscriminadamente.
- Su estructura interna como dependencia obligatoria.

**Decisión recomendada:** tratar SpiderFoot como proveedor intercambiable de resultados, no como el núcleo de tu plataforma.

---

## 2.2. Repositorios especializados por módulo

Para el resto de la plataforma, recomiendo los siguientes:

| Módulo | Repositorio | Qué utilizar | Qué evitar |
|---|---|---|---|
| Reconocimiento empresarial | [theHarvester](https://github.com/laramies/theHarvester?utm_source=chatgpt.com) | Descubrimiento de correos corporativos, dominios y fuentes | Recolección sin alcance definido |
| Superficie de ataque | [OWASP Amass](https://github.com/owasp-amass/amass?utm_source=chatgpt.com) | Enumeración y asociación de infraestructura | Descubrimiento activo no autorizado |
| Subdominios | [Subfinder](https://github.com/projectdiscovery/subfinder?utm_source=chatgpt.com) | Fuentes pasivas y resultados estructurados | Equiparar subdominio descubierto con activo propio |
| Reconocimiento modular | [Recon-ng](https://github.com/lanmaster53/recon-ng?wt5asdY0cyCbO=b51vVBPba25yO1u&utm_source=chatgpt.com) | Organización de módulos y fuentes | Dependencia de su arquitectura interna |
| Usuarios públicos | [Maigret](https://github.com/soxoj/maigret?utm_source=chatgpt.com) | Detección de perfiles candidatos | Confirmar identidades por coincidencia de username |
| Automatización OSINT | [sn0int](https://github.com/kpcyrd/sn0int?utm_source=chatgpt.com) | Diseño modular de recolección | Adoptar licencias o módulos sin revisarlos |
| Metadatos | [ExifTool](https://github.com/ExifTool/exiftool?utm_source=chatgpt.com) | Extracción de metadatos de archivos | Publicación indiscriminada de metadatos sensibles |
| Grafos interactivos | [Cytoscape.js](https://github.com/cytoscape/cytoscape.js/?utm_source=chatgpt.com) | Visualización, navegación y filtrado | Renderizar miles de nodos simultáneamente |
| Análisis de grafos | [NetworkX](https://github.com/networkx/networkx?utm_source=chatgpt.com) | Caminos, centralidad, componentes y comunidades | Confundir proximidad matemática con relación real |
| Comparación de identidades | [RapidFuzz](https://github.com/rapidfuzz/RapidFuzz?utm_source=chatgpt.com) | Comparación textual y generación de candidatos | Fusiones automáticas por similitud de nombre |
| Procesamiento distribuido | [Celery](https://github.com/celery/celery?utm_source=chatgpt.com) | Tareas, workers y reintentos | Introducir infraestructura distribuida prematuramente |
| Representaciones semánticas | [Sentence Transformers](https://github.com/huggingface/sentence-transformers?utm_source=chatgpt.com) | Comparación semántica y clasificación documental | Tratar similitud de embeddings como prueba de identidad |

Estos proyectos cubren funciones diferentes y pueden integrarse progresivamente. Por ejemplo, Amass y Subfinder permiten implementar proveedores alternativos de descubrimiento de subdominios, mientras que RapidFuzz y los modelos semánticos pueden generar candidatos de correlación mediante métodos distintos. [GitHub](https://github.com/owasp-amass/amass?utm_source=chatgpt.com)

### Otras referencias interesantes

**[Investigraph](https://github.com/investigraph/investigraph?utm_source=chatgpt.com)** es una referencia para extracción multilingüe de entidades y navegación de relaciones documentales, aunque se presenta como proyecto de investigación en beta.

**[Forenix OSS](https://github.com/thunderstornX/forenix-oss?utm_source=chatgpt.com)** resulta especialmente relevante para desarrollar trazabilidad, integridad de evidencias y registros de auditoría.

**[Kipi](https://github.com/assafkip/kipi?utm_source=chatgpt.com)** ofrece ideas para combinar grafos e investigación documental asistida por IA. Debe revisarse su licencia antes de incorporar código.

**[vis-network](https://github.com/visjs/vis-network?utm_source=chatgpt.com)** es una alternativa para representar redes interactivas. Para este proyecto, elegiría Cytoscape.js como primera opción.

### Mi selección para la arquitectura

No construiría el sistema sobre un fork monolítico de SpiderFoot o Aleph.

Construiría un núcleo propio con contratos estables y utilizaría las herramientas existentes como proveedores independientes.

| Componente | Elección inicial |
|---|---|
| Backend | Python + FastAPI |
| Frontend | React + TypeScript |
| Grafos visuales | Cytoscape.js |
| Persistencia | PostgreSQL |
| Ontología | Modelo propio compatible con FollowTheMoney |
| Grafos analíticos | NetworkX |
| Procesamiento de trabajos | Worker Python independiente con persistencia |
| Búsqueda | PostgreSQL Full Text Search |
| ML inicial | scikit-learn + RapidFuzz |
| Documentos | Extractores Python + ExifTool |
| Recolección OSINT | Adaptadores sobre herramientas existentes |
| Testing | pytest + Playwright |
| Despliegue | Docker Compose |
| Integración con agentes | CLI y REST; MCP no obligatorio |

**La decisión arquitectónica más importante es que cada conector, modelo y motor de procesamiento sea sustituible.** El núcleo debe seguir funcionando aunque desaparezca cualquiera de las herramientas externas.

El MVP utilizará PostgreSQL sin necesitar Neo4j, Redis ni OpenSearch. Estos últimos quedarán contemplados como extensiones, activables cuando las necesidades reales lo justifiquen.

---

# 3. Prompt maestro para el agente de desarrollo

El prompt PROJECT_CONTENTS.md está diseñado para entregarse directamente a Claude Code, Codex u OpenCode.

Incluye instrucciones de implementación, referencias a repositorios concretos, arquitectura, contratos, entregables, definición de terminado por fase y mecanismos para impedir que el agente declare funcionalidades completadas sin demostrarlo.

---

# 4. Evaluación final del planteamiento

El prompt cubre las funcionalidades principales de tu propuesta inicial y añade requisitos de ingeniería que considero necesarios para evitar problemas habituales en proyectos desarrollados mediante agentes.

| Criterio | Cobertura |
|---|---|
| Recolección OSINT modular | Completa |
| Referencias GitHub por módulo | Completa |
| Múltiples proveedores por capacidad | Completa |
| Resiliencia ante errores | Completa |
| Estado visual de herramientas | Completa |
| Grafo de conocimiento | Completa |
| Correlación y resolución de entidades | Completa |
| Evidencias y procedencia | Completa |
| Automatización de investigaciones | Completa |
| Prevención de bucles | Completa |
| Documentos e imágenes | Completa |
| Entrenamiento de modelos | Completa |
| Modelos generativos opcionales | Completa |
| APIs e interfaz web | Completa |
| Entrega modular | Completa |
| DoD verificable por fase | Completa |
| Continuidad entre agentes | Completa |
| Seguridad y privacidad | Completa |
| Pruebas y CI/CD | Completa |

La cobertura es **a nivel de especificación**. La viabilidad y compatibilidad de cada integración deberán demostrarse durante el desarrollo.

## 5. Tres decisiones que mantendría

**Primera: no hacer depender la plataforma de SpiderFoot.** Puede ser una fuente importante de descubrimientos, pero una arquitectura centrada en sus módulos limitaría tu capacidad para incorporar proveedores diferentes.

**Segunda: dar prioridad absoluta al grafo y a las evidencias.** Una plataforma que ejecuta cincuenta herramientas y devuelve cincuenta archivos es menos útil que una que ejecuta cinco, correlaciona correctamente sus resultados y permite explicar cada relación.

**Tercera: separar la evaluación de proveedores del entrenamiento de modelos.** Son problemas distintos. El primero determina qué herramientas funcionan mejor; el segundo busca mejorar tareas como la resolución de entidades, la clasificación y la valoración de evidencias. Ambos deben tener métricas y conjuntos de evaluación propios.

### El cambio más importante respecto a tu propuesta original

Introduciría un componente explícito que podría convertirse en el verdadero diferenciador comercial del proyecto:

**Investigation Intelligence Engine (IIE).**

Su responsabilidad sería evaluar continuamente cuatro cuestiones:

- **Qué sabemos:** entidades, relaciones y evidencias confirmadas.
- **Qué desconocemos:** contradicciones, información incompleta y relaciones candidatas.
- **Qué podemos investigar:** capacidades disponibles, fuentes permitidas y alcance autorizado.
- **Qué merece la pena investigar:** valor esperado, coste, fiabilidad y probabilidad de aportar información nueva.

Esto permitiría evolucionar desde una colección de herramientas OSINT hacia una plataforma capaz de **planificar y justificar investigaciones reproducibles**, manteniendo al analista en control de las decisiones que requieren revisión humana.