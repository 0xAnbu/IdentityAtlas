# PROMPT MAESTRO — INTELFABRIC

## 0. Rol, misión y reglas de ejecución

Actúa como **arquitecto principal de software, ingeniero de datos, ingeniero ML/MLOps, especialista OSINT empresarial, ingeniero de seguridad y responsable de QA**. Tu objetivo es IMPLEMENTAR, probar y documentar en este repositorio una plataforma modular, autoalojable y extensible de inteligencia de fuentes abiertas empresarial denominada provisionalmente **IntelFabric**. No entregues únicamente una propuesta o un prototipo visual: entrega software ejecutable, con pruebas y evidencias de funcionamiento.

**Visión:** soportar investigaciones OSINT *wide*, *deep*, focalizadas, continuas y orientadas a decisiones mediante perfiles de misión declarativos. Combinar fuentes heterogéneas, documentos, imágenes, metadatos, ML, DL, embeddings, modelos generativos y grafos. El mismo núcleo debe poder reutilizarse para superficie de ataque, due diligence, CTI, proveedores, documentos, protección de marca, riesgos y análisis temporal.

**Prioridades, por orden:** (1) respeto al alcance, finalidad, licencias y privacidad; (2) evidencia y reproducibilidad; (3) resiliencia verificable; (4) modularidad y mantenibilidad; (5) precisión y control de falsos positivos; (6) observabilidad visual; (7) eficiencia; (8) riqueza funcional. No sacrifiques una prioridad superior para mejorar otra inferior.

**Reglas no negociables:**
- Trabaja por fases, sin declarar una fase terminada hasta superar su DoD y entregar sus artefactos. Mantén siempre el repositorio arrancable y los tests anteriores en verde.
- Antes de reutilizar código ajeno, comprueba repo canónico, licencia de la versión concreta, mantenimiento, dependencias, superficie de seguridad y límites de distribución/uso comercial. Regístralo en `docs/REFERENCES.md` y `docs/THIRD_PARTY.md`. Referenciar una arquitectura no autoriza copiar su código.
- No inventes evidencia, cobertura, disponibilidad de conectores, benchmarks ni resultados de pruebas. Si no puedes ejecutar algo, documenta exactamente la limitación y mantén el trabajo como pendiente.
- Un *perfil* no concede autorización para actuar sobre entidades de terceros. Toda operación se somete a autorización real y a las condiciones de su fuente.
- No conviertas automáticamente una pista sobre un proveedor, filial, persona, cliente, IP compartida o dominio vecino en un nuevo objetivo autorizado.
- No pongas herramientas de ejecución arbitraria, red sin restricciones, shell ni credenciales privilegiadas a disposición de un LLM. Los modelos proponen acciones; un motor de políticas independiente las autoriza o deniega.
- No uses MCP como requisito de funcionamiento. Prefiere interfaces Python, CLI bien delimitada y HTTP/REST. No añadas Kubernetes, Kafka, Elasticsearch, Neo4j o microservicios salvo que exista una necesidad medida y registrada mediante ADR.
- No recopiles datos personales innecesarios ni utilices material recopilado para entrenamiento de forma automática. Los datos públicos NO implican por sí solos permiso para cualquier tratamiento.
- Si faltan claves, GPU o conectividad externa, el núcleo y una demo con datos sintéticos deben seguir funcionando. No marques resultados simulados como obtenidos en Internet.
- No solicites confirmación para decisiones menores: adopta los defaults de este documento y registra los supuestos. Solicita aprobación solo para acciones de alcance, legales o de alto impacto.

## 1. Referencias externas: tomar y no tomar

Antes de cada módulo relacionado, consulta su referencia canónica y anota la versión/revisión utilizada. No clones plataformas enteras para mezclarlas sin necesidad.

| Área | Referencias | Tomar | NO tomar |
|---|---|---|---|
| OSINT modular | https://github.com/smicallef/spiderfoot ; https://github.com/blacklanternsecurity/bbot | módulos, eventos, descubrimientos encadenados, outputs estructurados | crawling o escaneo recursivo sin política ni distinción pasivo/activo; copiar AGPL sin analizar obligaciones |
| Enriquecimiento/resiliencia | https://github.com/intelowlproject/IntelOwl | analizadores, pivots, ingestors, estado y health check por plugin | acoplar todo al modelo CTI o incorporar AGPL sin decisión jurídica |
| OSINT de dominios | https://github.com/projectdiscovery/subfinder ; https://github.com/owasp-amass/amass ; https://github.com/laramies/theHarvester | diversidad de fuentes, modos pasivos, salidas normalizables | asumir propiedad por simple descubrimiento; activar enumeración agresiva/activa por defecto |
| Conocimiento empresarial | https://github.com/openaleph/openaleph ; https://github.com/alephdata/followthemoney | ingesta documental, esquemas de entidades, investigación y relaciones | exigir el stack completo de OpenAleph; mezclar sin revisar licencias por subproyecto |
| CTI | https://github.com/OpenCTI-Platform/opencti ; https://github.com/OpenCTI-Platform/connectors ; https://github.com/MISP/MISP | STIX 2.1 en CTI, conectores, procedencia, intercambio | imponer STIX a toda la ontología empresarial; instalar dos suites CTI completas por defecto |
| PDF/Office | https://github.com/docling-project/docling ; https://github.com/Unstructured-IO/unstructured | extracción alternativa de documentos, tablas y estructura | obligar a ejecutar ambos para cada fichero o suponer equivalencia perfecta |
| OCR/visión | https://github.com/PaddlePaddle/PaddleOCR ; https://github.com/tesseract-ocr/tesseract | OCR alternativo y pruebas de calidad por idioma y documento | identificación biométrica ni análisis de personas indiscriminado |
| NLP/semántica | https://github.com/explosion/spaCy ; https://github.com/huggingface/sentence-transformers ; https://github.com/qdrant/fastembed | NER, clasificación, embeddings, reranking y evaluación | declarar identidad confirmada por similitud semántica |
| Web | https://github.com/adbar/trafilatura | extracción de contenido HTML y metadatos | permitir que el extractor decida el alcance de navegación |
| Workflow/agentes | https://github.com/PrefectHQ/prefect ; https://github.com/langchain-ai/langgraph | DAGs, reintentos, estados recuperables y supervisión humana | múltiples orquestadores para lo mismo; dar autoridad de políticas a un agente |
| Políticas/modelos | https://github.com/open-policy-agent/opa ; https://github.com/BerriAI/litellm | autorización independiente; routing/fallback de LLM | pensar que los prompts de seguridad o los guardrails del proveedor reemplazan el aislamiento |
| MLOps | https://github.com/mlflow/mlflow ; https://github.com/treeverse/dvc ; https://github.com/HumanSignal/label-studio ; https://github.com/evidentlyai/evidently | experimentos, datasets, anotación, evaluación y drift | reentrenar sin consentimiento, etiquetas auditadas ni validación independiente |
| LLM observabilidad | https://github.com/Arize-ai/phoenix ; https://github.com/open-telemetry/opentelemetry-python | trazas, evaluaciones y correlación por run | depender de Phoenix sin revisar ELv2 ni capturar prompts sensibles sin redacción |
| Grafo/estado visual | https://github.com/cytoscape/cytoscape.js ; https://github.com/TwiN/gatus | exploración del grafo y patrones de supervisión de disponibilidad | confundir salud de la web con salud de cada conector, capacidad y modelo |

**Aviso de licencias:** considera por separado código, modelos, pesos, datos, APIs y contenidos de terceros. AGPL-3.0, ELv2, licencias de modelos y licencias de datasets imponen obligaciones diferentes. Por ejemplo, https://github.com/opensanctions/opensanctions distribuye código MIT y datos con condiciones que pueden incluir uso no comercial: nunca deduzcas derechos de entrenamiento de la licencia del código. El repositorio histórico https://github.com/alephdata/aleph no es la base preferida para nueva integración: su equipo principal ha anunciado el fin del soporte. Estas notas son advertencias a verificar, no asesoramiento jurídico automático.

## 2. Arquitectura, stack y límites

**Stack inicial obligatorio:** monorepo; backend Python 3.12+ con FastAPI, Pydantic y SQLAlchemy/Alembic; PostgreSQL con búsqueda full-text y extensión pgvector cuando esté disponible; almacén de objetos S3-compatible (MinIO en desarrollo); worker Python; orquestación Prefect, sin añadir otro orquestador general; frontend React + TypeScript + Vite con Cytoscape.js; OpenTelemetry; MLflow y DVC para experimentos/datasets; OPA como servicio independiente de decisión de políticas. Utiliza Docker Compose con perfiles `core`, `ml` y `optional`; ejecución local CPU sin API de pago. Explica en un ADR cualquier cambio de stack.

**Capas y responsabilidades:**
1. **Control plane:** proyectos/tenants, fines, perfiles, scope, permisos, límites, aprobaciones, políticas, auditoría.
2. **Workflow plane:** DAGs, scheduling, colas, estados, reintentos, backpressure, checkpoints, cancelación, idempotencia.
3. **Acquisition plane:** broker de red, conectores, clasificación pasivo/target-facing/activo, cumplimiento de condiciones de fuentes.
4. **Processing plane:** parsers, OCR, visión, NLP, clasificación, extracción de metadatos, normalización.
5. **Intelligence plane:** resolución de entidades, relaciones, hipótesis, verificación, búsqueda semántica, agentes limitados.
6. **Evidence plane:** objetos originales con hash, extracciones versionadas, fuentes, temporalidad, auditoría y linaje.
7. **Presentation plane:** investigaciones, evidencias, grafo, resultados, alertas, salud, comparador de motores y MLOps.

No necesitas un grafo BD separado al inicio: entidades/aristas/procedencia en PostgreSQL y Cytoscape.js para visualización; documenta cuándo tendría sentido introducir un grafo dedicado. Mantén separado el índice vectorial del almacenamiento de hechos y evidencia. No asumas que pgvector es el sistema de verdad.

**Contratos de dominio (modelo versionado):** `Tenant`, `User`, `Role`, `Project`, `Investigation`, `MissionProfile`, `ApprovedScope`, `PolicyDecision`, `Source`, `Artifact`, `Extraction`, `Observation`, `Claim`, `Entity`, `EntityAlias`, `Relationship`, `Hypothesis`, `Contradiction`, `ToolManifest`, `ToolRun`, `HealthProbe`, `WorkflowRun`, `DatasetSnapshot`, `Annotation`, `ModelVersion`, `Experiment`, `Alert`, `AuditEvent`.

Cada afirmación y relación tiene `source_id`, referencia exacta al fragmento/página/objeto, `sha256`, método, versión del extractor/modelo, timestamps de adquisición y publicación (distinguirlos), validez cuando se conoce, estado (`observed`, `inferred`, `refuted`, `uncertain`) y confianza con su semántica documentada. Una afirmación sin evidencia no debe renderizarse como hecho. Preserva originales y permite recalcular derivados sin alterar el origen.

## 3. Perfiles de misión: contrato obligatorio

Cada perfil versionado YAML/JSON debe declarar: `objective`, `allowed_seed_types`, `scope`, `source_allowlist`, `source_denylist`, `collection_mode`, `graph_hops`, `max_redirects`, `data_types`, `processor_chain`, `model_candidates`, `privacy_policy`, `training_eligibility`, `budget`, `time_window`, `scheduling`, `evidence_requirements`, `human_approval_rules`, `outputs`, `stop_conditions` y `quality_metrics`. Validación estricta con schema y políticas por tenant.

**Perfiles predefinidos que se entregarán gradualmente, todos con la misma arquitectura:**
1. `wide_company_baseline`: huella empresarial general.
2. `passive_attack_surface`: dominios/subdominios/certificados/infraestructura publicada.
3. `shadow_it`: activos y servicios antiguos o de titularidad incierta.
4. `information_exposure`: documentos y datos empresariales expuestos.
5. `technology_stack`: tecnologías y dependencias declaradas/observables pasivamente.
6. `redteam_intelligence`: hipótesis previas a evaluación expresamente autorizada.
7. `cti_enrichment`: inteligencia de amenazas y correlación contextual.
8. `incident_timeline`: reconstrucción de información pública en una ventana temporal.
9. `third_party_risk`: proveedores, dependencias y concentración.
10. `corporate_due_diligence`: estructura societaria y riesgo público.
11. `brand_impersonation`: dominios y marcas aparentemente suplantados.
12. `reputation_watch`: noticias y controversias con deduplicación.
13. `regulatory_watch`: publicaciones de fuentes regulatorias autorizadas.
14. `competitive_intelligence`: productos y señales competitivas públicas.
15. `acquisition_intelligence`: adquisiciones, alianzas y subsidiarias.
16. `document_intelligence`: PDF, Office, tablas y contenido estructurado.
17. `visual_intelligence`: imágenes, logos y OCR empresarial (sin identificación biométrica).
18. `geospatial_corporate`: sedes/instalaciones publicadas y su evolución.
19. `metadata_intelligence`: metadatos de documentos y su procedencia.
20. `entity_network`: entidades, vínculos e incertidumbre.
21. `continuous_watch`: seguimiento incremental y alertas.
22. `executive_exposure`: exposición corporativa estrictamente minimizada y autorizada; sin dossiers personales amplios.
23. `focused_question`: respuesta trazable con criterio de suficiencia.
24. `hypothesis_verification`: evidencias a favor/en contra de una afirmación.
25. `historical_comparison`: análisis temporal empresarial.

**Perfil adicional separado:** `authorized_validation`, deshabilitado de fábrica y disponible solo con ROE, activos, ventanas y acciones aprobadas explícitamente. No lo mezcles con `passive_attack_surface`.

Las plantillas de perfiles se entregan con un `capability_matrix`: `working`, `partially_available`, `requires_credentials`, `not_implemented` o `blocked_by_policy`. No llames «soportado» a un perfil sin un flujo end-to-end real y tests. En la primera release basta con varios perfiles operativos y el resto claramente etiquetado hasta su fase de entrega.

## 4. Redundancia de herramientas y comparador (doble resiliencia)

**Regla central:** para cada *capacidad intercambiable* se registran al menos dos implementaciones reales **cuando sean técnica y legalmente comparables**. No cuentan dos nombres que llaman al mismo servicio subyacente, ni dos mocks, ni un proveedor que exige una credencial ausente como redundancia disponible.

Matriz inicial de candidatos:
- Subdominios pasivos: Subfinder / Amass en modo pasivo / fuentes propias autorizadas (CT, RDAP, APIs). Referencias: Subfinder y Amass. NO usar acciones target-facing sin aprobación.
- Enriquecimiento de observables: IntelOwl / adaptadores directos de fuentes CTI autorizadas. NO dependencia obligatoria de una instancia IntelOwl.
- Extracción PDF/Office: Docling / Unstructured. NO mezclar tablas de ambos sin resolver correspondencia y procedencia.
- OCR: Tesseract / PaddleOCR. NO asumir que ambos ofrecen igual precisión o formato de salida.
- HTML: Trafilatura / parser HTML estructural de respaldo (BeautifulSoup o selectolax). NO dar al parser permisos de navegación.
- NER/clasificación: spaCy / modelos Transformers compatibles. NO presentar como prueba una etiqueta generada por modelo.
- Embeddings: Sentence Transformers / FastEmbed, con compatibilidad de dimensión/índice por modelo. NO mezclar embeddings de modelos distintos en un mismo índice lógico.
- LLM: dos proveedores/modelos configurables mediante LiteLLM, con opción local y política explícita de transmisión de datos. NO enviar automáticamente documentos a proveedores externos.
- Inferencia de relaciones: reglas deterministas / modelo supervisado. NO equiparar score con evidencia.
- Metadatos: parser propio fiable de formatos seleccionados / ExifTool en sandbox, cuando esté instalado y permitido. NO ejecutar comandos arbitrarios.

Implementa interfaces tipadas `AdapterManifest`, `AdapterHealth`, `ScopedRequest`, `EvidenceResult`, `CapabilityResolver`, `PolicyDecision`, `EvaluationResult`. Todo adaptador declara: ID, versión, tipo de capacidad, entradas/salidas compatibles, fuentes/proveedores, tipo de tráfico, permisos, dependencias, licencias, costes, limitaciones y métodos `healthcheck`, `execute`, `cancel` y `normalize_result` cuando correspondan.

**Modos del resolver:**
- `fallback`: proveedor principal, backoff y circuit breaker, y alternativo permitido solo ante errores recuperables.
- `benchmark`: misma entrada y dataset de evaluación, diferentes implementaciones, resultados separados y medidos sin mezclar evidencias.
- `ensemble`: fusionar resultados compatibles mediante reglas explícitas, con procedencia por motor.
- `manual_override`: fijar proveedor para reproducir un caso.

**Reglas de failover:** una denegación por scope, credenciales, política, finalidad, licencia o privacidad NO se sortea cambiando de proveedor; aplicar *fail closed*. Para rate limit/timeouts/5xx, aplicar presupuesto global de reintentos, jitter, cooldown, circuit breaker y fallback permitido. Asegurar idempotencia y no reintentar indefinidamente. Si caen todos los proveedores, devolver `PARTIAL`/`UNAVAILABLE` con huecos de cobertura, nunca resultados ficticios.

**Estados de salud:** `HEALTHY`, `DEGRADED`, `UNAVAILABLE`, `AUTH_REQUIRED`, `RATE_LIMITED`, `POLICY_BLOCKED`, `DISABLED`, `UNKNOWN`, `STALE`. Salud != éxito de ejecución != calidad del resultado; modelar estas tres dimensiones por separado. Guardar última comprobación, latencia, errores, dependencias, duración de incidencia y motivo legible. Emitir eventos para la UI. Ref: IntelOwl para health checks y Gatus para patrones visuales; NO reutilizar un único semáforo global que oculte fallos individuales.

## 5. Seguridad y fronteras de confianza

**Referencia:** OPA para decisiones independientes, BBOT/SpiderFoot para entender expansión; NO usar una instrucción LLM como frontera de seguridad.

- `PolicyEngine` deniega por defecto si falta scope, autorización o está caído el servicio de políticas. Revalidar al preparar el trabajo y justo antes de cada operación de red, adquisición, ejecución de herramienta o exportación.
- Distinguir `third_party_passive` (APIs/fuentes externas), `target_read_only` (acceso directo a infraestructura del objetivo) y `active_validation`. Solo la primera categoría está permitida por defecto y aun así depende de la política de la fuente.
- Broker de red con controles contra SSRF: normalizar URL, esquema y puerto; prohibir credenciales embebidas; resolver y verificar A/AAAA; controlar DNS rebinding y redirecciones hop a hop; bloquear loopback, link-local, IP internas, metadatos cloud y destinos no aprobados mediante validación de aplicación **y aislamiento de red/egress**. No permitir que subprocesses/CLI eviten el broker.
- Sandbox para documentos y ejecutables auxiliares: límites de CPU, memoria, tiempo, tamaño, profundidad de archivo, descompresión y acceso al sistema; no `shell=True`, no ejecución de macros ni scripts extraídos.
- Contenido web, HTML, repositorios, OCR, metadatos y documentos son datos no confiables y pueden contener prompt injection. Separar instrucciones de contenido, etiquetar procedencia, validar salidas estructuradas, redacción de secretos y nunca obedecer acciones embebidas.
- LLM sin navegación ilimitada, shell, acceso al sistema de archivos arbitrario ni secretos en contexto; exclusivamente *tools* mediadas por servidor. Si un agente solicita nueva URL o entidad, validarla antes de ejecutar.
- RBAC por tenant y proyecto; aislamiento en BD, API, objetos, caché, índices de búsqueda, datasets, modelos y trazas. Incluir tests de fuga entre tenants.
- Datos personales: finalidad/base jurídica evaluada, minimización, redacción, acceso restringido, retención configurable, eliminación y revisión de DPIA cuando corresponda. No construir reconocimiento facial indiscriminado.
- Etiqueta legal/licencia y permiso de procesamiento/entrenamiento/exportación por artefacto y fuente; bloqueo automatizado cuando falte el permiso requerido.
- Secretos en variables/secret store, nunca logs, prompts, artefactos de entrenamiento ni reportes.
- Auditoría append-only de decisiones, acciones, aprobaciones y cambios en políticas; cancelación y revocación de tareas en ejecución.

**Pruebas adversariales obligatorias:** prompt injection en HTML/PDF/OCR/metadata; URL de tercero fuera de scope; enlace con redirección a IP privada; DNS rebinding simulado; ZIP/PDF bomb limitado; proveedor caído; salida LLM malformada; ampliación recursiva a tercero; request cross-tenant; caída de OPA; leak de prompt/traza; rate limit; reintentos/ciclos. Resultado obligatorio: acceso denegado y evidencia registrada donde corresponda.

## 6. Datos, ML/DL, entrenamiento y evaluación

**Referencias:** MLflow, DVC, Label Studio, Evidently, spaCy, Sentence Transformers, FastEmbed, Docling/PaddleOCR. **Tomar:** rastreo de experimentos, datasets, anotación, evaluación. **NO tomar:** entrenamiento automático con todos los datos recopilados ni resultados sin *holdout*.

Separa estrictamente `raw_artifacts` -> `normalized_observations` -> `eligible_training_examples` -> `reviewed_labels` -> `dataset_snapshot` -> `model_experiment` -> `registered_model` -> `deployment`. La ingesta **NO** habilita entrenamiento por defecto. Cada fuente define elegibilidad para entrenamiento, base de autorización, licencia, consentimiento/base jurídica cuando aplique, región, vencimiento y condiciones de borrado. Versionar datasets y código de preprocesamiento con hash y linaje.

Capacidades entrenables mínimas:
1. Clasificador de relevancia/tema de documentos: dos baselines reales (p. ej. TF-IDF + LogisticRegression y TF-IDF + RandomForest o LinearSVC); entrenar con muestra elegible y etiquetada, evaluar y registrar el ganador.
2. Resolución de entidades corporativas: baseline de reglas frente a modelo supervisado si hay etiquetas válidas; medir precisión, recall y falsas fusiones.
3. Comparación OCR: Tesseract frente a PaddleOCR con muestras etiquetadas, CER/WER y latencia; no prometer entrenar pesos de cualquier OCR si su pipeline no lo soporta. Documentar coste y viabilidad de fine-tuning como capacidad especializada.
4. Recuperación semántica: dos encoders de Sentence Transformers/FastEmbed, mismo conjunto de consultas etiquetadas, Recall@k/MRR y latencia; ajustar modelos solo si el formato y los derechos lo permiten.
5. Modelos generativos: evaluación de extracción de claims, fidelidad a fuentes, citas y abstenciones. Fine-tuning opcional únicamente si hay datos elegibles suficientes y aprobación; RAG no equivale a entrenar.

Validaciones: split por empresa/entidad y/o tiempo para evitar fuga de datos; conjuntos train/validation/test inmutables; control de duplicados cercanos; métricas por idioma y formato; matriz de confusión, precisión, recall y F1 según tarea; calibración cuando se muestre probabilidad; evaluación de privacidad y ataques a modelos. Nunca elegir un modelo por una sola métrica o por una prueba con datos del entrenamiento.

**Champion/challenger:** versión registrada, criterios de promoción reproducibles, rollback, shadow evaluation y aprobación humana para cambios de alto impacto. Monitorizar drift y degradación, sin auto-promoción por defecto. Toda retirada de datos por derechos o licencia afecta datasets derivados y exige analizar la retirada, inhabilitación o reentrenamiento de modelos; borrar un registro de BD NO garantiza que un modelo ya entrenado olvide su contenido.

**Salida:** API/CLI y UI para crear datasets elegibles, solicitar etiquetado, lanzar experimentos, comparar modelos por calidad/latencia/recursos/coste, seleccionar champion y auditar la promoción. Tests con dataset sintético público en el repositorio; tests reales sólo con datos permitidos.

## 7. Inteligencia, correlación y agentes

**Referencias:** FollowTheMoney/OpenAleph para entidades; OpenCTI para CTI y STIX; LangGraph para agentes con checkpoints. **NO tomar:** un solo esquema CTI para todo, ni autonomía sin límites.

Modelo de conocimiento con entidad canónica + alias + posibles coincidencias + relaciones + evidencias. Proporciona desambiguación, fusiones reversibles, vínculos hipotéticos, contradicciones, fechas, *confidence* y explicaciones. Similitud visual o semántica genera candidatos, NO hechos. Evitar saltos de grafo fuera de alcance; candidatos ajenos se conservan solo como referencias mínimas pendientes de aprobación.

Los agentes generativos solo podrán: clasificar documentos, extraer afirmaciones con spans, resumir evidencia, sugerir hipótesis, proponer consultas a fuentes aprobadas y preparar informes con citas verificadas. Cada respuesta devuelve JSON validado contra esquema, citas fuente-fragmento y estado `supported`, `uncertain`, `unsupported`. Un verificador independiente comprueba que cada referencia existe y respalda materialmente la afirmación; no se acepta cita inventada. Fijar profundidad máxima, tokens, coste, cantidad de tools y límite temporal por ejecución. Checkpoint y cancelación.

Proporciona *focused question* con criterio de suficiencia, *deep dive* con límites de saltos y *continuous watch* con comparación incremental. Un informe debe incluir cobertura real, lagunas, evidencia contradictoria y fecha de observación.

## 8. UI y experiencia de operación

**Referencias:** IntelOwl para estado de analizadores, Cytoscape.js para el grafo, Gatus para página de disponibilidad, MLflow para experimentos. **NO tomar:** dashboards estáticos o que representen UNKNOWN como disponible.

Vistas funcionales: (1) Home con proyectos/investigaciones; (2) constructor y validador de perfiles de misión; (3) gestor de scope y aprobaciones; (4) catálogo de capacidades/conectores/modelos; (5) matriz de disponibilidad; (6) ejecución en vivo por etapas; (7) explorador de evidencias, documentos, imágenes y metadatos; (8) grafo interactivo temporal; (9) búsqueda y preguntas con fuentes; (10) monitorización/alertas; (11) laboratorio MLOps y comparación de modelos; (12) auditoría y administración.

**Requisito visual central:** el estado de CADA proveedor debe aparecer por nombre, capacidad, icono/color más texto, última comprobación, causa, acción necesaria (`configurar API key`, `instalar`, `rate limit`, `error`, `bloqueado por política`), latencia y fallback elegido. Mostrar impacto por investigación y porcentaje de cobertura *estimado y justificado*. `DISABLED` y `AUTH_REQUIRED` no son fallos técnicos; `UNKNOWN` no es verde. Mostrar ejecución parcial y errores sin ocultarlos tras el éxito de otra herramienta. Historial de salud y eventos de failover.

La UI debe demostrar, en un test e2e, que al provocar la caída de `provider_A` cambia su estado, aparece el fallback a `provider_B`, el usuario ve un aviso y el pipeline continúa con evidencias válidas; al caer ambos la vista marca `PARTIAL/UNAVAILABLE` y no fabrica hallazgos. Si OPA deniega, la UI muestra `POLICY_BLOCKED` y ninguna petición se ejecuta.

Usa SSE para progreso/estado unidireccional desde el servidor y REST para comandos; evita WebSockets si no hay necesidad bidireccional justificada. Respeta accesibilidad básica (teclado, contraste, textos de estado, errores claros), paginación, filtros y virtualización para grandes colecciones.

## 9. API, interoperabilidad y exportación

**Referencias:** IntelOwl para APIs de análisis, OpenCTI/MISP para CTI y FollowTheMoney para entidades. **NO tomar:** una API universal que pierda semántica o evidencias.

Contrato OpenAPI y errores tipados. Endpoints mínimos versionados: `/api/v1/projects`, `/profiles`, `/scope`, `/policy/check`, `/investigations`, `/runs`, `/runs/{id}/events` (SSE), `/capabilities`, `/providers`, `/providers/{id}/health`, `/artifacts`, `/claims`, `/entities`, `/relationships`, `/graph`, `/search`, `/alerts`, `/datasets`, `/experiments`, `/models`, `/audit`, `/exports`. Implementar authn/authz y paginación, filtrado por tenant, idempotency keys, rate limiting e IDs de correlación.

Exportaciones: JSON y CSV con evidencias; informe Markdown/HTML; formato FollowTheMoney compatible cuando proceda; STIX 2.1 exclusivamente para objetos CTI semánticamente compatibles. Nunca exportar datos excluidos por política, secretos ni datos de otro tenant.

## 10. Operación, calidad y rendimiento

**Referencias:** Prefect para reintentos/recuperación; OpenTelemetry para trazas; Evidently para drift; Gatus para salud. **NO tomar:** health checks que solo prueben si el proceso está vivo, ni métricas sin etiquetas de proyecto/ejecución.

Instalación reproducible con `docker compose --profile core up --build` (o comando único equivalente documentado), migraciones y datos de demo sintéticos. Ninguna credencial externa ni GPU obligatoria. `Makefile` o `taskfile` con `bootstrap`, `up`, `down`, `seed`, `lint`, `typecheck`, `test`, `test-integration`, `test-e2e`, `test-security`, `benchmark`, `docs`.

Observabilidad: logs estructurados con secretos redactados, trazas por run, métricas de latencia, tasa de fallo por conector, errores de parseo, volumen útil, retries, éxito de fallback, costes/tokens, tamaño de colas, uso CPU/RAM, bytes procesados, cambios detectados, edad de fuentes y calidad de modelos. Alarmas configurables.

CI: Ruff, formatter, mypy/pyright donde proceda, pytest, cobertura de lógica crítica, frontend lint/typecheck, integración con servicios efímeros, Playwright para escenarios UI, análisis de dependencias/SBOM y detección de secretos. Pruebas sin red externa reproducibles con fixtures sintéticas y simuladores de fallo; smoke externo opt-in y nunca dentro de CI por defecto.

Métricas de calidad: 100% de tests de seguridad P0 y de contratos críticos pasando; cobertura de ramas crítica objetivo >=90% donde tenga sentido; ninguna vulnerabilidad crítica conocida sin mitigación; 0 salidas de scope en fixtures adversariales; trazabilidad comprobable para cada hecho presentado; cada perfil operativo con flujo e2e; pruebas de carga con hardware y dataset documentados, tasas y percentiles medidos, y sin regresiones no justificadas. No afirmar «producción lista» solo porque Compose arranca.

## 11. Estructura mínima del repositorio

```text
intelfabric/
  apps/api/                 # FastAPI, auth, control plane, contratos
  apps/web/                 # React/TypeScript, visualización y estados
  workers/                  # ingestión, procesamiento, training
  packages/core/            # esquema, DTO, evidencias y políticas
  packages/adapters/        # implementaciones, manifests, healthcheck
  packages/intelligence/    # entidades, grafo, claims, search, RAG
  packages/ml/              # datasets, training, evaluation, registry
  profiles/                 # 25 perfiles versionados y matrices de cobertura
  policies/                 # OPA y pruebas de políticas
  infra/                    # Docker Compose, migraciones, telemetría
  fixtures/synthetic/       # demos reproducibles y ataques simulados
  tests/unit/
  tests/integration/
  tests/e2e/
  tests/security/
  tests/performance/
  docs/                     # arquitectura, threat model, ADR, handoff, DoD
  .github/workflows/
  Makefile
  README.md
```

Ajusta nombres solo si justificas una mejora técnica. No crees directorios vacíos simulando implementaciones.

## 12. Plan de entrega por fases, con DoD contractual

**Regla de cada fase:** producir commit(s), implementación funcional, tests, documentación y `docs/phases/PHASE-N.md` con: objetivo, alcance realizado, decisiones, evidencias (comandos/salidas), archivos modificados, demo reproducible, riesgos, limitaciones reales, issues y criterios DoD `PASS/FAIL/BLOCKED`. Cualquier fase `BLOCKED` NO cuenta como completada. No avances ocultando defectos P0.

### Fase 0 — Descubrimiento técnico y contratos
**Referencias:** revisar todos los repos anteriores, especialmente SpiderFoot, IntelOwl, BBOT, OpenAleph y OPA. **Tomar:** patrones verificables. **Evitar:** copiar arquitectura completa, APIs obsoletas y dependencias con licencias incompatibles.
**Entregables:** `docs/ARCHITECTURE.md`, `docs/THREAT_MODEL.md`, `docs/REFERENCES.md` con versiones y licencias, `docs/THIRD_PARTY.md`, ADRs, diagramas, schemas iniciales, backlog mapeado a capacidades y matriz de riesgos.
**DoD:** cada decisión de stack tiene rationale, alternativa descartada y coste; amenazas y límites de confianza documentados; matriz de licencias y datos existe; esquema de perfil, adaptador y evidencia validable; tareas de fases dependientes identificadas.

### Fase 1 — Núcleo ejecutable, identidad y almacenamiento
**Referencias:** OpenAleph/FollowTheMoney (datos), Prefect (trabajos). **Tomar:** separación de ingestión/datos. **Evitar:** stack de 10 servicios no necesarios.
**Entregables:** Compose `core`, API FastAPI, web mínima funcional, PostgreSQL, MinIO, migraciones, login/roles, tenants, proyectos, investigaciones, esquema de evidencias y fixture sintética.
**DoD:** arranque desde cero con un comando; migraciones ida/vuelta probadas; lectura/escritura de un artefacto y su hash; acceso cruzado denegado por tests; OpenAPI real; `pytest` y lint verdes.

### Fase 2 — Policies, scope y broker de adquisición
**Referencias:** OPA, BBOT, SpiderFoot. **Tomar:** políticas independientes y clasificación de acciones. **Evitar:** expansión autónoma y autorización mediante prompt.
**Entregables:** servicio PolicyEngine, reglas OPA, scope versionado, clasificador de actividad, broker HTTP seguro, aprobación humana, bitácora, pruebas SSRF/redirecciones/DNS.
**DoD:** intentos fuera de scope, IP interna, falta de autorización y caída de OPA se bloquean; ninguna red de conectores contornea el broker; cambios de scope auditados; e2e de denegación exitoso.

### Fase 3 — Adaptadores, redundancia y salud
**Referencias:** IntelOwl, Subfinder, Amass, LiteLLM, Gatus. **Tomar:** manifests, plugins, health, fallbacks. **Evitar:** suponer disponibles proveedores sin claves ni silenciar errores.
**Entregables:** SDK de adaptadores, registry, resolver `fallback/benchmark/ensemble/manual`, circuit breaker, health checks y API de estado; dos implementaciones reales para una primera capacidad; simuladores de fallo deterministas.
**DoD:** caída de principal => alternativo permitido; caída total => `UNAVAILABLE`; error de policy => sin fallback; latencia/causa visibles vía API; idempotencia y budgets cubiertos por tests.

### Fase 4 — Adquisición pasiva empresarial
**Referencias:** Subfinder, Amass pasivo, theHarvester, SpiderFoot, BBOT, Trafilatura. **Tomar:** variedad de fuentes y formatos. **Evitar:** escaneos activos, crecimiento sin límite del grafo y eludir condiciones de APIs.
**Entregables:** conectores reales para al menos dos rutas pasivas comparables cuando estén disponibles; importación de snapshots, CT/RDAP/fuentes permitidas, documentos HTML, deduplicación, provenance, `wide_company_baseline`, `passive_attack_surface` y `focused_question` operativos sobre demo.
**DoD:** de una semilla demo se obtienen activos con su evidencia y tiempos; fuente sin clave reporta `AUTH_REQUIRED`; se registran huecos de cobertura; políticas aplican también a redirecciones y subprocesos; pruebas de 2 rutas y fallos verdes.

### Fase 5 — Documentos, imágenes y metadatos
**Referencias:** Docling/Unstructured, PaddleOCR/Tesseract, Trafilatura. **Tomar:** extracción multimodal alternativa y métricas. **Evitar:** ejecutar contenido activo y fingir que un OCR equivale a otro.
**Entregables:** ingestión PDF/Office/HTML/imagen con límites, documento original, parser alternativo, OCR dual, tablas, citas página/fragmento, metadatos, detección/redacción de PII/secrets, pruebas con corpus sintético.
**DoD:** fallback real ante parser que falla; OCR comparado con CER/WER si hay ground truth; hash y fragmentos recuperables; ZIP/PDF bomb detenido; `document_intelligence`, `metadata_intelligence` y `visual_intelligence` operativos sobre sus fixtures.

### Fase 6 — Entidades, grafo, búsqueda y evidencia
**Referencias:** FollowTheMoney, OpenAleph, OpenCTI, Cytoscape.js, Sentence Transformers/FastEmbed. **Tomar:** entidades, relaciones, interoperabilidad y grafo visual. **Evitar:** hacer hechos de similitudes, imponer STIX a todo.
**Entregables:** ontología versionada, resolución de entidades, relaciones y contradicciones, búsqueda full-text/vectorial, API graph, vista Cytoscape, timeline, exportación compatible cuando aplique.
**DoD:** relaciones enlazadas a evidencia; fusiones reversibles; pruebas de homónimos/IP compartida sin falsas fusiones automáticas; índice vectorial separado por modelo/tenant; grafo navegable en e2e.

### Fase 7 — Datasets, modelos entrenables y evaluación
**Referencias:** MLflow, DVC, Label Studio, Evidently, spaCy, Sentence Transformers. **Tomar:** linaje, entrenamiento real, benchmarks y registro. **Evitar:** entrenamiento con datos sin derecho de uso o métricas sobre train.
**Entregables:** catálogo de elegibilidad, snapshots versionados, integración de anotación, pipeline de extracción de features, dos baselines entrenados de clasificación, tests train/validation/test, tabla comparativa, registry, operación de promoción/rollback.
**DoD:** un usuario entrena sobre dataset elegible y etiquetado (demo sintética por defecto), ve métricas y artefactos reales, compara dos modelos, promociona uno manualmente y lo usa en un pipeline; un dato sin permiso no entra; splits sin leakage; MLflow registra experimento y DVC huella del dataset.

### Fase 8 — LLM/RAG y agentes contenidos
**Referencias:** LiteLLM, LangGraph, OPA, OpenTelemetry. **Tomar:** modelos intercambiables, ejecución persistente y trazas. **Evitar:** navegador libre, shell, secretos, loops y autoridades implícitas.
**Entregables:** broker LLM, selección de modelos, fallback condicionado, RAG con ACL, extracción de claims JSON, verificador de citas, analista de hipótesis, prompts versionados, inyección adversarial y presupuesto.
**DoD:** respuestas con citas reales o abstención; intentos de prompt injection no saltan scope; no filtración cross-tenant; agotar tokens/steps detiene el flujo; modelo offline no disponible => estado visible sin inventar respuesta; evaluación versionada.

### Fase 9 — Dashboard operativo, fallos visuales y monitorización
**Referencias:** IntelOwl, Gatus, Cytoscape.js, Prefect. **Tomar:** salud por herramienta y progresión por pipeline. **Evitar:** un único badge global, mocks mostrados como fuentes reales.
**Entregables:** todas las vistas indicadas en sección 8 con funciones respaldadas por API, estados `HEALTHY/DEGRADED/...`, SSE, historial de fallos, comparador de herramientas y modelos, alertas, cancelación.
**DoD:** pruebas Playwright muestran caída de A, fallback a B, caída de ambos, bloqueo por policy y recuperación; estado/causas/huecos de cobertura visibles sin refresco manual; UI accesible y soporta grandes resultados paginados.

### Fase 10 — Catálogo completo de casos de uso y ejecución continua
**Referencias:** SpiderFoot/BBOT (módulos), OpenCTI/MISP (CTI), OpenAleph/FtM (empresarial), Prefect (scheduling). **Tomar:** componentes compartidos y fuentes especializadas. **Evitar:** 25 YAML sin workflows reales.
**Entregables:** 25 manifiestos con matriz de cobertura honesta; implementación incremental de workflows, empezando por CTI, proveedores, marca, due diligence, cambios e hipótesis; monitorización incremental, comparación histórica, alertas y exportadores; perfil `authorized_validation` separado, deshabilitado y protegido.
**DoD:** para cada perfil marcado `working`, fixture, salida y e2e específicos; perfiles incompletos identificados claramente con causas, nunca anunciados como finalizados; comparación histórica y alertas sin duplicados; pruebas de alcance y licencias específicas por familia. Para declarar la fase COMPLETA, los 25 perfiles deben alcanzar `working` con fuentes permitidas/fixtures pertinentes; los que requieran claves externas deben funcionar al menos mediante una ruta alternativa permitida y demostrar `AUTH_REQUIRED` en la ruta no configurada. Si esto no se alcanza, marcar la fase `PARTIAL/BLOCKED` y detallar brechas; no falsear el DoD.

### Fase 11 — Hardening y release reproducible
**Referencias:** OPA, OpenTelemetry, Prefect, Evidently, MLflow. **Tomar:** auditoría, evaluaciones y recuperación. **Evitar:** promesa de escalabilidad sin benchmarks.
**Entregables:** CI completa, SBOM, escaneo de dependencias, backups/restauración, migraciones, guía operacional, ejercicios de fallos, métricas de carga, manual de usuario, despliegue documentado, changelog y release etiquetada.
**DoD:** instalación desde cero por otra persona/sandbox; restauración completa verificada; pruebas P0 100%; tests e2e y seguridad ejecutados con logs; benchmark con CPU/RAM, throughput y p95; licencia de cada dependencia y dataset evaluada; demos de dos escenarios completos; ningún secreto incluido en repo.

## 13. DoD global, criterios de parada y formato de comunicación

**Definition of Done transversal:** funcionalidad real y accesible; contrato tipado; políticas verificadas; datos trazables; pruebas unitarias/integración/e2e y adversariales pertinentes; UI refleja estado real; alternativa/fallback cuando la capacidad sea redundante; docs de uso y límites; observabilidad; licencias; evidencia ejecutada. Sin uno de ellos, NO «DONE».

**Plan de trabajo por tarea:** `ID`, fase, objetivo, dependencias, archivos, referencia GitHub y patrón concreto (tomar/no tomar), pruebas esperadas, riesgos y outputs. Entregar código en incrementos verticales pequeños. Prohibido sumar funcionalidad fuera de fase si arriesga la entrega actual. Usa ADRs para compromisos mayores y feature flags para lo experimental.

**Al cerrar cada fase, comunica exactamente:**
1. `Estado: PASS / FAIL / BLOCKED`.
2. `Entregables`: rutas concretas.
3. `Funciones demostradas`: casos y evidencias.
4. `Verificación`: comandos ejecutados, salidas resumidas, tests y fallos reales.
5. `Seguridad y scope`: decisiones permitidas/bloqueadas verificadas.
6. `Resiliencia`: proveedor A/B, estado de health y resultado al simular fallos.
7. `Métricas`: calidad, cobertura real, coste/latencia si procede.
8. `Pendientes`: bloqueos, deuda técnica y riesgo.
9. `Siguiente fase`: dependencias y criterios de inicio.

**Contrato de finalización del proyecto:** no declarar «completo» hasta que todos los DoD de fase estén en `PASS`; los 25 perfiles tengan workflows probados, el núcleo sea reproducible sin APIs pagadas, existan dos implementaciones comparables por cada capacidad indicada como redundante, el entrenamiento sobre datos elegibles funcione, los modelos sean comparables y reversibles, la supervisión visual sea honesta, las reglas de seguridad se prueben y la guía de reproducción permita ejecutar las demos desde cero. Un fallo de servicio, modelo o fuente solo debe degradar las capacidades dependientes; una caída del motor de autorización debe bloquear operaciones sensibles de forma segura.

**Empieza ahora por la Fase 0.** Reconoce el contenido existente del repositorio (si lo hay) antes de modificarlo; no borres trabajo válido. Identifica decisiones técnicas y plan de fases; implementa lo que puedas con pruebas reales. Continúa fase por fase únicamente después de verificar y registrar los criterios de salida. No prometas trabajo futuro: produce los artefactos de la fase actual en esta ejecución y reporta bloqueos con precisión.