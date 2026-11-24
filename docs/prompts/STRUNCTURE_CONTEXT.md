# 1\. Repositorios de GitHub que utilizaría como referencia

He localizado proyectos que cubren partes importantes de la plataforma que quieres construir: automatización OSINT, reconocimiento empresarial, correlación de inteligencia, análisis documental, ML/DL, entrenamiento, orquestación y supervisión de herramientas.

**Mi conclusión es que no elegiría un único repositorio para ampliarlo.** Construiría una plataforma propia que reutilizara componentes existentes mediante adaptadores, tomando las mejores decisiones arquitectónicas de varios proyectos.

## 1.1. Los repositorios más relevantes

Evaluación basada en la documentación pública y repositorios consultados el 22 de noviembre de 2026. La compatibilidad y las licencias deben comprobarse nuevamente antes de incorporar código.

| Proyecto | Encaje | Qué aprovecharía y qué evitaría |
|--------|--------|--------|
| [SpiderFoot](https://github.com/smicallef/spiderfoot) | Muy alto | Sus más de 200 módulos y el intercambio de eventos entre ellos. No copiaría su enfoque de investigación recursiva como política universal. [github.comgithub.com](https://github.com/smicallef/spiderfoot/blob/master/README.md) |
| [BBOT](https://github.com/blacklanternsecurity/bbot) | Muy alto | Arquitectura modular, eventos, reconocimiento recursivo, API Python y salidas estructuradas. No trasladaría su comportamiento de escáner a todos los perfiles: algunas operaciones requieren autorización adicional. [github.com](https://github.com/blacklanternsecurity/bbot)[github.com](https://github.com/blacklanternsecurity/bbot/blob/stable/README.md) |
| [IntelOwl](https://github.com/intelowlproject/IntelOwl) | Muy alto | Analizadores intercambiables, ejecución mediante API, ingestors, pivots, visualizadores y comprobaciones de salud por plugin. No limitaría la plataforma a observables de CTI. [github.com](https://github.com/intelowlproject/IntelOwl/blob/master/README.md)[github.com](https://github.com/intelowlproject/docs/blob/main/docs/IntelOwl/usage.md) |
| [OpenAleph](https://github.com/openaleph/openaleph) | Muy alto | Indexación de documentos, búsqueda de entidades, investigación sobre grandes colecciones y colaboración. No copiaría todo su stack ni asumiría que sus componentes tienen una única licencia. [github.com](https://github.com/openaleph/openaleph)[github.com](https://github.com/openaleph/openaleph-search) |
| [OpenCTI](https://github.com/OpenCTI-Platform/opencti) | Alto | Grafo de conocimiento, conectores, trazabilidad de inteligencia y modelo STIX 2.1. No impondría STIX como modelo universal para información corporativa. [github.com](https://github.com/OpenCTI-Platform/opencti)[github.com](https://github.com/OpenCTI-Platform/opencti/blob/master/README.md) |
| [FollowTheMoney](https://github.com/alephdata/followthemoney) | Muy alto | Esquemas de entidades y relaciones para investigaciones empresariales: sociedades, activos, personas, documentos y estructuras de propiedad. No convertiría una relación inferida en un hecho confirmado. [github.com](https://github.com/alephdata/followthemoney)[alephdata.github.io](https://alephdata.github.io/followthemoney/docs/) |
| [OWASP Amass](https://github.com/owasp-amass/amass) | Alto | Descubrimiento de activos, fuentes de información y correlación de dominios. No habilitaría sus funciones activas en perfiles estrictamente pasivos. [github.com](https://github.com/owasp-amass/amass) |
| [Subfinder](https://github.com/projectdiscovery/subfinder) | Alto | Enumeración pasiva de subdominios y diversidad de proveedores de información. No usaría sus resultados como prueba automática de propiedad. [github.com](https://github.com/projectdiscovery/subfinder) |
| [theHarvester](https://github.com/laramies/theHarvester) | Alto | Diversidad de fuentes para descubrir dominios y datos corporativos relevantes. No habilitaría por defecto las opciones de comprobación activa ni la recopilación indiscriminada de información personal. [github.com](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1)[github.com](https://github.com/laramies/theHarvester/blob/master/docs/wiki/Responsible-Use-and-Scope.md) |
| [MISP](https://github.com/MISP/MISP) | Medio-alto | Gestión de indicadores, intercambio de inteligencia y formatos de exportación CTI. No convertiría todo el sistema en una plataforma centrada exclusivamente en indicadores de amenazas. [github.com](https://github.com/misp/misp)[github.com](https://github.com/MISP/MISP) |

### Mi elección entre los cinco principales



**SpiderFoot — referencia para el motor OSINT**

Su patrón de módulos productores y consumidores de eventos se ajusta al objetivo de realizar descubrimientos encadenados. Lo adaptaría a perfiles limitados por alcance y profundidad.

---



**IntelOwl — referencia para resiliencia y plugins**

Es especialmente relevante porque ya contempla analizadores, visualizadores, pivots y health checks. Lo tomaría como referencia para la supervisión visible de integraciones.

---



**OpenAleph — referencia para investigación documental**

Resulta apropiado para el tratamiento de grandes colecciones, entidades y evidencias que deben mantenerse accesibles a través de búsquedas.

---



**OpenCTI — referencia para conocimiento correlacionado**

Aprovecharía sus ideas de estructuración, interoperabilidad y visualización de relaciones. Mantendría un modelo empresarial independiente del dominio CTI.

---



**BBOT — referencia para descubrimiento y pipelines modulares**

Interesa por su diseño orientado a extensiones y eventos. Evitaría heredar sus políticas operativas sin adaptarlas a cada misión.

## 1.2. Componentes para ML, DL y procesamiento multimodal

Aquí ya no buscamos una plataforma OSINT completa, sino **motores especializados que puedas sustituir, comparar y entrenar cuando técnicamente corresponda**\.

| Capacidad | Repositorios | Papel en tu sistema |
|--------|--------|--------|
| Documentos | [Docling](https://github.com/docling-project/docling) y [Unstructured](https://github.com/Unstructured-IO/unstructured) | Dos estrategias de extracción de PDF, Office, tablas y documentos estructurados. [github.com](https://github.com/docling-project/docling)[github.com](https://github.com/Unstructured-IO/unstructured) |
| OCR | [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) y [Tesseract](https://github.com/tesseract-ocr/tesseract) | Comparación de precisión, rendimiento, idiomas y recuperación ante fallos. [github.com](https://github.com/PaddlePaddle/PaddleOCR/)[github.com](https://github.com/tesseract-ocr/tesseract) |
| NLP y NER | [spaCy](https://github.com/explosion/spaCy) y [Transformers](https://github.com/huggingface/transformers) | Extracción, clasificación y entrenamiento de modelos para entidades corporativas. [github.com](https://github.com/explosion/spacy) |
| Embeddings | [Sentence Transformers](https://github.com/huggingface/sentence-transformers) y [FastEmbed](https://github.com/qdrant/fastembed) | Búsqueda semántica, comparación y evaluación de modelos de representación. [github.com](https://github.com/huggingface/sentence-transformers)[github.com](https://github.com/qdrant/fastembed/blob/main/README.md) |
| Extracción web | [Trafilatura](https://github.com/adbar/trafilatura) | Extracción de contenido y metadatos web, separada de la política de navegación. [github.com](https://github.com/adbar/trafilatura) |
| Entrenamiento y registro | [MLflow](https://github.com/mlflow/mlflow) | Experimentos, métricas, artefactos, evaluación y registro de versiones de modelos. [github.com](https://github.com/mlflow/mlflow) |
| Versionado de datasets | [DVC](https://github.com/treeverse/dvc) | Trazabilidad de conjuntos de datos, pipelines reproducibles y experimentos. [github.com](https://github.com/treeverse/dvc) |
| Etiquetado | [Label Studio](https://github.com/HumanSignal/label-studio) | Revisión humana y generación de conjuntos de entrenamiento supervisados. [github.com](https://github.com/HumanSignal/label-studio/) |
| Evaluación y drift | [Evidently](https://github.com/evidentlyai/evidently) | Métricas de calidad, desviación de datos y supervisión de modelos. [github.com](https://github.com/evidentlyai/evidently) |
| Evaluación generativa | [Phoenix](https://github.com/Arize-ai/phoenix) | Trazabilidad y evaluación de aplicaciones LLM; revisar sus condiciones ELv2 antes de integrarlo. [github.com](https://github.com/arize-ai/phoenix)[github.com](https://github.com/Arize-ai/phoenix) |

## 1.3. Componentes para orquestación, seguridad y visualización

| Repositorio | Qué aprovecharía |
|--------|--------|
| [Prefect](https://github.com/PrefectHQ/prefect) | Workflows Python, reintentos, planificación y observabilidad de tareas. [github.com](https://github.com/PrefectHQ/prefect) |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Ejecución persistente de procesos con agentes, estado recuperable y revisiones humanas. No lo utilizaría como motor global de permisos. [github.com](https://github.com/langchain-ai/langgraph) |
| [Open Policy Agent](https://github.com/open-policy-agent/opa) | Autorización independiente del LLM, mediante políticas declarativas. [github.com](https://github.com/open-policy-agent/opa/blob/main/README.md) |
| [LiteLLM](https://github.com/BerriAI/litellm) | Unificación de proveedores de modelos, routing, presupuestos y failover. [github.com](https://github.com/BerriAI/litellm-docs/blob/main/docs/routing.md)[github.com](https://github.com/BerriAI/litellm/blob/main/README.md) |
| [Gatus](https://github.com/TwiN/gatus) | Comprobaciones de disponibilidad, alertas y patrones para un panel de estado. |
| [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-python) | Trazas y métricas de las llamadas a herramientas, pipelines y modelos. [github.com](https://github.com/open-telemetry/opentelemetry-python) |
| [Cytoscape.js](https://github.com/cytoscape/cytoscape.js) | Visualización interactiva de relaciones y grafos empresariales. [github.com](https://github.com/cytoscape/cytoscape.js) |

## 1.4. Advertencias importantes sobre reutilización

Tres hallazgos modifican directamente la arquitectura que recomendaría\:

**1\. No tomaría el Aleph original como dependencia central nueva.** El repositorio `alephdata/aleph` advierte de la finalización del soporte por su equipo principal. Para un proyecto nuevo estudiaría OpenAleph y FollowTheMoney, verificando el estado de cada componente. [github.com](https://github.com/alephdata/aleph/blob/develop/README.rst)[github.com](https://github.com/openaleph/openaleph)

**2\. No asumiría que todos los repositorios permiten la misma reutilización comercial.** BBOT, IntelOwl y MISP utilizan AGPL-3.0, mientras que SpiderFoot, Docling, FollowTheMoney y otros componentes tienen licencias más permisivas. Incorporar código AGPL en un producto ofrecido por red puede tener consecuencias de distribución y disponibilidad de código fuente que deben evaluarse. [github.com](https://github.com/blacklanternsecurity/bbot)[github.com](https://github.com/intelowlproject)[github.com](https://github.com/MISP/MISP)[github.com](https://github.com/docling-project/docling)

**3\. Código abierto no significa datos abiertos para cualquier finalidad.** OpenSanctions, por ejemplo, licencia su código bajo MIT, pero buena parte de los datos producidos bajo CC BY-NC 4.0, y algunos materiales de terceros tienen condiciones diferentes. Esto importa especialmente si quieres comercializar el producto o entrenar modelos con datos recopilados. [github.com](https://github.com/opensanctions/opensanctions)

Por tanto, el prompt debe obligar al agente a mantener un registro de licencias, condiciones de fuentes, procedencia de datasets y restricciones de entrenamiento.

---

# 2\. Prompt maestro para implementar la plataforma

He preparado el prompt completo en Markdown, listo para entregarlo a Claude Code, Codex, OpenCode u otro agente de desarrollo con acceso al repositorio.

### PROMPT MAESTRO — INTELFABRIC

Markdown · 5.319 palabras · 12 fases · 25 perfiles operativos

:chatgpt-content-reference{index="69"}[Descargar prompt maestro completo (.md)](sandbox:/mnt/data/PROMPT_MAESTRO_INTELFABRIC.md)

Incluye arquitectura, contratos de interfaces, referencias GitHub, componentes que reutilizar y evitar, requisitos funcionales, pruebas, fases, entregables y Definition of Done.

## 2.1. Qué exige el prompt

El agente no puede limitarse a crear interfaces o ejecutar herramientas OSINT. Tiene que implementar la plataforma y demostrar su funcionamiento mediante pruebas.

| Requisito | Garantía exigida |
|--------|--------|
| Versatilidad | 25 perfiles de misión, con contratos declarativos, alcance y resultados diferenciados. |
| Redundancia | Múltiples implementaciones por capacidad comparable y mecanismos de fallback verificables. |
| Comparación | Mismos datasets y métricas reproducibles para comparar herramientas y modelos. |
| Entrenamiento | Datasets versionados, etiquetado, entrenamiento real, evaluación y registro de modelos. |
| Resiliencia | Circuit breakers, retries, checkpoints, recuperación y degradación controlada. |
| Visibilidad | Estado individual de herramientas, dependencias, errores, fallbacks y cobertura efectiva. |
| Seguridad | Policy engine independiente, bloqueo de acciones fuera de alcance, aislamiento y pruebas adversariales. |
| Calidad | Tests automatizados, trazabilidad de evidencias, métricas y validación de resultados. |
| Entrega | 12 fases con artefactos, pruebas, demostraciones y DoD individuales. |

## 2.2. Contrato de entrega por fases

SECUENCIA DE DESARROLLO

1. **Fase 0 — Arquitectura y contratos**
   
   ADRs, modelo de amenazas y evaluación de licencias
2. **Fase 1 — Núcleo ejecutable**
   
   API, base de datos, autenticación y frontend mínimo
3. **Fase 2 — Políticas y alcance**
   
   OPA, broker de red y controles de autorización
4. **Fase 3 — Adaptadores y resiliencia**
   
   Proveedores alternativos, fallback y health checks
5. **Fase 4 — Adquisición empresarial**
   
   Conectores pasivos e inventario de activos
6. **Fase 5 — Procesamiento multimodal**
   
   Documentos, imágenes, OCR y metadatos
7. **Fase 6 — Correlación y conocimiento**
   
   Entidades, grafo, evidencias y búsqueda
8. **Fase 7 — Entrenamiento ML/DL**
   
   Datasets, experimentos, comparación y model registry
9. **Fase 8 — Agentes generativos**
   
   LLM/RAG con herramientas restringidas y citas verificables
10. **Fase 9 — Dashboard y monitorización**
    
    Estados visuales, fallos, métricas y alertas
11. **Fase 10 — Casos de uso completos**
    
    25 perfiles y workflows especializados
12. **Fase 11 — Hardening y release**
    
    CI, auditoría, benchmarks y despliegue reproducible

Cada fase incluye en el archivo los repositorios de referencia, qué aprovechar de ellos, qué evitar, entregables concretos y criterios verificables de finalización.

## 2.3. Dos decisiones que considero especialmente importantes

**No confundir redundancia con disponibilidad real.** Si tienes Subfinder y Amass configurados, pero ambos dependen de la misma fuente externa caída, no dispones necesariamente de dos vías independientes. El prompt exige registrar dependencias y comprobar que las alternativas realmente funcionan.

**No confundir recopilación con entrenamiento.** El sistema puede almacenar millones de documentos, pero eso no significa que todos puedan o deban utilizarse para entrenar modelos. El prompt separa adquisición, elegibilidad legal, etiquetado, dataset, entrenamiento, evaluación y despliegue. También contempla el impacto de retirar datos que ya se utilizaron para entrenar.

Por último, el contrato establece que **una fase incompleta no puede declararse terminada**\. Si un conector no funciona, faltan credenciales, un modelo no supera las pruebas o una funcionalidad está simulada, el agente debe hacerlo explícito en los entregables y en la interfaz.

El archivo es la especificación íntegra para iniciar el desarrollo; la tabla anterior es únicamente un mapa de su contenido.