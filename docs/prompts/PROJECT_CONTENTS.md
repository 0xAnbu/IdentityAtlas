# PROYECTO: OSINT INTELLIGENCE PLATFORM

## 0. TU MISIÓN

Actúa como arquitecto principal de software, ingeniero Python senior, especialista en OSINT, ingeniero de datos y responsable de calidad.

Debes diseñar e implementar una plataforma local-first de inteligencia de fuentes abiertas (OSINT) basada en:

1. Recolección modular de información.
2. Integración de herramientas OSINT existentes.
3. Normalización de resultados heterogéneos.
4. Gestión de evidencias y procedencia.
5. Resolución conservadora de entidades.
6. Correlación automática entre datos.
7. Representación mediante grafos interactivos.
8. Investigación automatizada mediante reglas.
9. Múltiples herramientas alternativas por capacidad.
10. Observabilidad y recuperación ante errores.
11. Análisis de documentos, imágenes y metadatos.
12. Entrenamiento y evaluación de modelos de machine learning.
13. Integración opcional de modelos generativos.
14. Generación de informes reproducibles.
15. Monitorización periódica y detección de cambios.

El resultado debe ser un **producto de software funcional, extensible y verificable**, no una colección de scripts independientes, un mockup o una demostración simulada presentada como aplicación completa.

### Principio fundamental

La plataforma debe diferenciar rigurosamente:

- `DISCOVERY`: encontrar registros potencialmente relevantes.
- `RESOLUTION`: determinar si varios registros corresponden a una misma entidad.
- `ENRICHMENT`: obtener información adicional a partir de una entidad y una relación justificadas.
- `CORRELATION`: descubrir relaciones entre observaciones.
- `VERIFICATION`: confirmar o refutar hipótesis mediante evidencias.
- `REPORTING`: presentar conclusiones auditables.

Una coincidencia textual, visual o estadística no constituye por sí sola una identidad confirmada.

### Modalidad de trabajo

Trabaja de manera incremental y autónoma.

No solicites confirmación entre fases si los requisitos permiten tomar una decisión razonable.

Cuando exista ambigüedad:

1. Evalúa las alternativas.
2. Selecciona la más sencilla que satisfaga los requisitos.
3. Registra la decisión.
4. Continúa con la implementación.

No reemplaces funcionalidades requeridas por simulaciones silenciosas.

No declares completada una fase hasta satisfacer su Definition of Done (DoD).

---

# 1. RESTRICCIONES GENERALES

## 1.1. Tecnología

Priorizar:

- Python para backend, conectores, orquestación y ML.
- FastAPI para API REST.
- React y TypeScript para frontend.
- PostgreSQL como base de datos inicial.
- Cytoscape.js para visualización.
- SQLAlchemy y Alembic para persistencia y migraciones.
- Pydantic para validación.
- pytest para pruebas.
- Playwright para pruebas end-to-end.
- Docker Compose para despliegue reproducible.

No introducir componentes distribuidos salvo que exista una necesidad funcional comprobable.

El sistema debe funcionar inicialmente en una única máquina Linux.

## 1.2. Modularidad

Cada módulo debe:

- Tener responsabilidades claramente delimitadas.
- Exponer interfaces documentadas.
- Ser reemplazable sin modificar otros módulos.
- Poder probarse independientemente.
- Declarar dependencias.
- Informar de su estado.
- Producir errores estructurados.
- Registrar métricas.
- Permitir ejecución aislada.

Prohibido crear un archivo monolítico que contenga toda la aplicación.

Prohibido introducir dependencias circulares.

## 1.3. Licencias

Antes de reutilizar código externo:

1. Inspecciona `LICENSE`.
2. Comprueba compatibilidad con el proyecto.
3. Comprueba restricciones de uso comercial.
4. Identifica las dependencias transitivas relevantes.
5. Documenta la decisión.

Distingue siempre entre:

- Referencia arquitectónica.
- Dependencia externa.
- Herramienta invocada mediante CLI.
- Biblioteca importada.
- Código adaptado.
- Dataset utilizado.

No copies código sin comprobar y respetar su licencia.

No asumas que una fuente de datos permite redistribución por ser públicamente accesible.

## 1.4. Seguridad y privacidad

El sistema se orienta a:

- Pentesting autorizado.
- Reconocimiento empresarial.
- Investigación corporativa legítima.
- Análisis de exposición digital propia.
- Investigación documental con fuentes permitidas.
- Investigación OSINT realizada bajo un alcance definido.

Toda investigación debe tener propósito y alcance.

Implementa restricciones de acceso a datos, retención y procesamiento.

No implementes una función genérica de perfilado invasivo de personas.

Excluye de la recolección automatizada general:

- Contraseñas.
- Tokens de autenticación.
- Credenciales bancarias.
- Identificadores gubernamentales de terceros.
- Mensajería privada.
- Contactos privados.
- Datos médicos.
- Identificadores biométricos para reconocimiento arbitrario.
- Inferencias de categorías especialmente protegidas.
- Localización en tiempo real o reconstrucción de rutinas privadas.

Cuando aparezcan accidentalmente datos prohibidos, aplica detección, minimización, cuarentena o descarte según la política definida.

Las consultas de exposición de cuentas deben exigir autorización o verificación aplicable.

Las fuentes con requisitos legales, contractuales o de autenticación específicos deben quedar deshabilitadas hasta configurarse correctamente.

---

# 2. REPOSITORIOS DE REFERENCIA

Antes de implementar el proyecto, inspecciona los repositorios siguientes.

No es necesario clonar todos.

Para cada repositorio utilizado, documenta:

- Problema que resuelve.
- Funcionalidades relevantes.
- Tecnología.
- Licencia.
- Estado de mantenimiento.
- Interfaces disponibles.
- Coste de integración.
- Código o arquitectura que se aprovechará.
- Funcionalidades que no deben copiarse.
- Decisión final: integrar, adaptar, utilizar como referencia o descartar.

## 2.1. Plataformas generales

### OpenOSINT

https://github.com/OpenOSINT/OpenOSINT

Aprovechar:

- Modelo de correlación.
- Evidencias asociadas a resultados.
- Grafo de entidades.
- Deduplicación no destructiva.
- Revisión humana.

No adoptar obligatoriamente MCP ni depender de agentes LLM.

### TRACE

https://github.com/denoflore/trace

Aprovechar:

- Gestión local de investigaciones.
- Importación de resultados.
- Revisión de duplicados.
- Visualización de entidades.
- Exportación GraphML/STIX.

No acoplar el backend a su interfaz.

### SpiderFoot

https://github.com/smicallef/spiderfoot

Aprovechar:

- Ecosistema de módulos.
- Descubrimiento de información.
- Clasificación de observaciones.
- Integración mediante interfaces documentadas.

No convertir SpiderFoot en el núcleo de la aplicación.

### Aleph

https://github.com/alephdata/aleph

Aprovechar:

- Indexación documental.
- Organización de colecciones.
- Búsqueda.
- Relaciones entre documentos y entidades.

No adoptar su infraestructura completa inicialmente.

### Forenix OSS

https://github.com/thunderstornX/forenix-oss

Aprovechar:

- Integridad de evidencias.
- Auditoría.
- Gestión reproducible de investigaciones.

### Investigraph

https://github.com/investigraph/investigraph

Aprovechar como referencia para:

- Extracción de entidades.
- Relaciones documentales.
- Análisis de corpus.

Evaluar su madurez antes de cualquier dependencia.

---

# 3. ARQUITECTURA DEL SISTEMA

Implementa la siguiente separación lógica.

```text
                  WEB UI / CLI / REST API
                            |
                     AUTHORIZATION
                            |
                      CASE MANAGER
                            |
                     INVESTIGATION API
                            |
                 INVESTIGATION ORCHESTRATOR
                            |
          +-----------------+-----------------+
          |                 |                 |
      SCHEDULER        POLICY ENGINE      TOOL REGISTRY
          |                 |                 |
          +-----------------+-----------------+
                            |
                      JOB EXECUTOR
                            |
                  CONNECTOR ADAPTERS
                            |
       +--------------------+--------------------+
       |                    |                    |
   WEB SOURCES         OSINT TOOLS          DOCUMENTS
       |                    |                    |
       +--------------------+--------------------+
                            |
                      RAW OBSERVATIONS
                            |
                   NORMALIZATION ENGINE
                            |
                    EVIDENCE MANAGEMENT
                            |
                ENTITY RESOLUTION ENGINE
                            |
                   KNOWLEDGE GRAPH
                            |
                 CORRELATION / ANALYTICS
                            |
                   ENRICHMENT PLANNER
                            |
                  REVIEW / APPROVAL GATE
                            |
              REPORTING / EXPORT / MONITORING
```

### Restricción arquitectónica

Ninguna herramienta externa debe escribir directamente en las tablas principales del grafo.

Todas deben producir observaciones mediante el mismo contrato.

El motor de correlación no debe ejecutar conectores.

El planificador puede proponer trabajos, pero solamente el orquestador autorizado podrá ejecutarlos.

Las reglas de autorización deben aplicarse tanto al planificar como al ejecutar.

---

# 4. ESTRUCTURA DEL REPOSITORIO

Crear una estructura equivalente a:

```text
osint-platform/
├── README.md
├── LICENSE
├── pyproject.toml
├── docker-compose.yml
├── .env.example
├── Makefile
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── auth/
│   │   ├── cases/
│   │   ├── connectors/
│   │   │   ├── base/
│   │   │   ├── corporate/
│   │   │   ├── infrastructure/
│   │   │   ├── profiles/
│   │   │   ├── exposure/
│   │   │   ├── documents/
│   │   │   └── images/
│   │   ├── normalization/
│   │   ├── evidence/
│   │   ├── entities/
│   │   ├── resolution/
│   │   ├── graph/
│   │   ├── orchestration/
│   │   ├── policies/
│   │   ├── models/
│   │   ├── analytics/
│   │   ├── monitoring/
│   │   ├── reporting/
│   │   └── infrastructure/
│   ├── migrations/
│   └── tests/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── graph/
│   │   ├── connectors/
│   │   ├── investigations/
│   │   ├── models/
│   │   └── services/
│   └── tests/
│
├── workers/
├── datasets/
│   ├── synthetic/
│   └── README.md
├── models/
├── scripts/
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DECISIONS.md
│   ├── CONNECTOR_SPEC.md
│   ├── ENTITY_MODEL.md
│   ├── SECURITY.md
│   ├── MODEL_TRAINING.md
│   ├── PROJECT_STATUS.md
│   ├── HANDOFF.md
│   ├── TEST_REPORT.md
│   ├── REFERENCES.md
│   └── phases/
│
└── .github/
    └── workflows/
```

Se permite modificar esta estructura cuando exista una justificación técnica documentada.

No crear directorios vacíos únicamente para aparentar avance.

---

# 5. MODELO DE DATOS

## 5.1. Referencia

Repositorio:

https://github.com/opensanctions/followthemoney

Utiliza FollowTheMoney como referencia ontológica.

Evalúa compatibilidad para importar y exportar entidades.

No necesitas incorporar su ontología completa durante el MVP.

## 5.2. Entidades

El sistema debe poder representar:

### Personas y organizaciones

- Person.
- Organization.
- Company.
- PublicOfficialRole.
- ProfessionalProfile.
- PublicAccount.
- BusinessRegistration.

### Identificadores digitales

- Email.
- Username.
- Domain.
- Subdomain.
- IPAddress.
- ASN.
- URL.
- PublicKey.
- Repository.
- Certificate.

### Documentación

- Document.
- Publication.
- Article.
- Image.
- Video.
- Audio.
- Dataset.
- SourceRecord.

### Infraestructura

- Host.
- Service.
- DNSRecord.
- Network.
- Technology.
- SecurityFinding.

### Relaciones

- ASSOCIATED_WITH.
- PUBLISHED_BY.
- MENTIONS.
- WORKS_FOR.
- CONTRIBUTED_TO.
- REGISTERED_TO.
- RESOLVES_TO.
- HOSTED_ON.
- OBSERVED_IN.
- SUPPORTED_BY.
- CONTRADICTS.
- POSSIBLY_SAME_AS.
- CONFIRMED_SAME_AS.

Las relaciones deben existir solamente cuando el caso y las evidencias permitan establecerlas.

No confundir una relación entre registros con una relación personal entre individuos.

## 5.3. Separación de conceptos

Implementar cuatro estructuras diferenciadas:

**Entity:** objeto conceptual identificado internamente.

**Observation:** información obtenida directamente de una fuente.

**Claim:** afirmación derivada de una o varias observaciones.

**Evidence:** elemento que permite justificar una observación o afirmación.

Una entidad puede tener varias afirmaciones contradictorias.

Las afirmaciones no deben sobrescribirse silenciosamente.

## 5.4. Esquema mínimo

```python
class Observation(BaseModel):
    id: UUID
    case_id: UUID
    connector_id: str
    connector_version: str

    subject_type: str
    predicate: str
    object_type: str | None
    observed_value: str

    source_url: str | None
    source_type: str
    source_record_id: str | None

    observed_at: datetime
    source_timestamp: datetime | None

    evidence_id: UUID | None
    raw_record_hash: str

    collection_status: str
    verification_status: str

    confidence: float | None

    schema_version: str
```

La implementación deberá ampliar el modelo con los campos necesarios de seguridad, retención, procedencia y auditoría.

### Requisitos

- IDs internos estables.
- Identificación de la investigación.
- Versionado del esquema.
- Trazabilidad de cada observación.
- Deduplicación.
- Soporte para contradicciones.
- Aislamiento entre investigaciones.
- Eliminación conforme a retención.
- Exportación de resultados.

### DoD de modelo

No se considera terminado hasta demostrar que:

1. Dos fuentes pueden afirmar valores diferentes sin perder información.
2. Dos entidades pueden mantenerse separadas pese a compartir nombre.
3. Una relación puede asociarse a varias evidencias.
4. Una observación puede rastrearse hasta su ejecución de origen.
5. Una entidad puede exportarse con sus relaciones y evidencias.

---

# 6. SISTEMA DE CONECTORES

## 6.1. Objetivo

Construir un sistema de plugins para integrar herramientas OSINT heterogéneas sin acoplamiento.

Cada herramienta debe implementar una interfaz común.

Ejemplo:

```python
class OSINTConnector(Protocol):

    @property
    def metadata(self) -> ConnectorMetadata:
        ...

    async def healthcheck(self) -> HealthStatus:
        ...

    async def execute(
        self,
        request: ConnectorRequest,
    ) -> ConnectorResult:
        ...

    async def cancel(self, job_id: str) -> None:
        ...
```

La interfaz definitiva podrá ampliarse, pero deberá conservar estas responsabilidades.

## 6.2. Metadatos obligatorios

Cada conector declarará:

```yaml
id: subfinder
name: Subfinder
version: "1.0"

capabilities:
  - domain_discovery

input_types:
  - domain

output_types:
  - subdomain

execution:
  type: subprocess
  timeout_seconds: 120

requirements:
  executable: subfinder

authentication:
  required: false

rate_limits:
  requests_per_minute: null

policy:
  active_network_interaction: false
  requires_scope: true

fallback:
  priority: 20
```

Los valores anteriores son ilustrativos.

No asumir que una herramienta o todas sus fuentes son pasivas sin verificar su configuración efectiva.

## 6.3. Registro dinámico

El sistema debe detectar:

- Conectores instalados.
- Conectores no instalados.
- Conectores mal configurados.
- Conectores deshabilitados.
- Conectores sin autorización.
- Conectores temporalmente fallidos.

Estados:

```text
AVAILABLE
UNAVAILABLE
MISCONFIGURED
DISABLED
UNAUTHORIZED
RATE_LIMITED
DEGRADED
FAILED
```

Distinguir el estado de disponibilidad del estado de una ejecución concreta.

## 6.4. Ejecución

Implementar:

- Timeouts.
- Reintentos controlados.
- Backoff exponencial con jitter.
- Circuit breakers.
- Cancelación.
- Límites de concurrencia.
- Captura de errores.
- Captura de resultados.
- Normalización.
- Registro de duración.
- Registro de versión.
- Protección contra ejecución arbitraria.

Para herramientas CLI:

- Utilizar argumentos estructurados.
- No utilizar `shell=True` con entradas del usuario.
- Restringir ejecutables mediante allowlist.
- Limitar recursos y tiempo.
- Evitar registrar credenciales.
- Aislar procesos cuando sea necesario.

## 6.5. Resiliencia mediante proveedores alternativos

Una capacidad debe poder tener múltiples implementaciones.

Ejemplo:

```yaml
capability: subdomain_discovery

providers:
  - id: subfinder
    priority: 10

  - id: amass_passive
    priority: 20

  - id: certificate_transparency
    priority: 30

execution_strategy: fallback

minimum_successful_providers: 1
```

Soportar:

- Fallback.
- Ejecución paralela.
- Ejecución secuencial.
- Quórum de proveedores.
- Comparación de resultados.

El sistema debe distinguir entre una fuente independiente y varias herramientas que utilizan el mismo proveedor de información.

Dos herramientas que consultan la misma fuente no constituyen necesariamente corroboración independiente.

### DoD

Demostrar mediante pruebas automatizadas que:

1. Un proveedor falla por timeout.
2. El sistema registra el error.
3. Otro proveedor compatible continúa la operación.
4. El resultado se normaliza correctamente.
5. La interfaz muestra el proveedor fallido.
6. La investigación no pierde su estado.
7. La política de alcance no se modifica durante el fallback.

---

# 7. CONECTORES OSINT INICIALES

## 7.1. Infraestructura

Referencias:

https://github.com/owasp-amass/amass

https://github.com/projectdiscovery/subfinder

https://github.com/laramies/theHarvester

https://github.com/smicallef/spiderfoot

Implementar adaptadores para:

- DNS público.
- Certificate Transparency.
- RDAP.
- Subfinder.
- Amass en modalidad pasiva permitida.
- theHarvester.

Implementar SpiderFoot posteriormente mediante una integración documentada.

Capacidades:

- Descubrimiento de dominios.
- Descubrimiento de subdominios.
- Relaciones DNS.
- Certificados.
- Registros de infraestructura.
- Referencias a correos corporativos públicos.

No ejecutar reconocimiento activo fuera del alcance autorizado.

## 7.2. Perfiles públicos

Referencia:

https://github.com/soxoj/maigret

Implementar descubrimiento de perfiles públicos candidatos.

Conservar:

- Username consultado.
- URL candidata.
- Fuente.
- Fecha.
- Resultado de verificación.
- Nivel de confianza.

No fusionar automáticamente personas por coincidencia de username.

Limitar búsquedas sobre personas a casos debidamente autorizados.

## 7.3. Empresas

Referencias:

https://github.com/opensanctions/followthemoney

https://github.com/alephdata/aleph

Implementar conectores o importadores para:

- Registros mercantiles públicos.
- Publicaciones corporativas.
- Documentos de empresas.
- Registros de contratación pública.
- Publicaciones oficiales.

Priorizar fuentes españolas y europeas.

Contemplar:

- BOE.
- BORME.
- Plataforma de Contratación del Sector Público.
- OpenCorporates, si sus condiciones de API lo permiten.
- Datos corporativos publicados por organismos oficiales.

No utilizar scraping donde esté prohibido.

No simular acceso gratuito a APIs comerciales.

## 7.4. Exposición digital

Implementar una interfaz para proveedores de notificación de filtraciones.

Proveedor inicial recomendado: Have I Been Pwned.

Requisitos:

- Autorización apropiada.
- Gestión de credenciales de API.
- Tratamiento únicamente de metadatos permitidos.
- Registro de incidentes.
- Categorías de información expuesta.
- Fecha de consulta.

No almacenar contraseñas filtradas ni volcados de credenciales.

Si una API requiere suscripción, mostrar claramente:

`UNAVAILABLE: API_KEY_REQUIRED`

El resto del sistema debe seguir funcionando.

---

# 8. NORMALIZACIÓN Y CORRELACIÓN

## 8.1. Normalización

Todos los resultados deben convertirse a observaciones tipadas.

Ejemplos:

```text
Maigret → PublicAccount
Subfinder → Subdomain
Certificate Transparency → Certificate / Domain
RDAP → DomainRegistration / Network
ExifTool → FileMetadata
Corporate Register → Company / Filing
```

Implementar validadores para:

- Dominios.
- IP.
- ASN.
- URLs.
- Emails.
- Fechas.
- Hashes.
- Identificadores internos.

Preservar siempre el dato original.

## 8.2. Resolución de entidades

Referencias:

https://github.com/rapidfuzz/RapidFuzz

https://github.com/opensanctions/followthemoney

Implementar inicialmente:

- Normalización textual.
- Coincidencias exactas.
- Comparación de atributos.
- Similitud de cadenas.
- Reglas de contradicción.
- Generación de candidatos.
- Aprobación humana.

Estados:

```text
UNRESOLVED
CANDIDATE_MATCH
CORROBORATED
VERIFIED
DISPUTED
REJECTED
```

La similitud textual no debe elevar automáticamente una coincidencia a `VERIFIED`.

## 8.3. Confianza

Distinguir:

- Calidad de la fuente.
- Calidad de la extracción.
- Confianza en la identidad.
- Confianza en la relación.
- Vigencia temporal.
- Independencia de las evidencias.

No reducir todas estas dimensiones a un único número sin documentar la metodología.

Si existe una puntuación agregada, conservar sus componentes.

## 8.4. Resolución de conflictos

Ejemplo:

```text
Fuente A:
Empresa X → Director Y

Fuente B:
Empresa X → Director Z
```

El sistema debe:

1. Almacenar ambas afirmaciones.
2. Registrar fechas.
3. Identificar posible contradicción.
4. Evaluar vigencia.
5. Mostrar ambas fuentes.
6. Permitir revisión.

No sobrescribir una afirmación por la última recuperada.

---

# 9. MOTOR DE INVESTIGACIÓN AUTOMÁTICA

## 9.1. Objetivo

Crear un planificador capaz de decidir qué pasos de investigación están justificados.

El sistema debe funcionar sin IA generativa.

Los LLM podrán proponer investigaciones adicionales, pero no sustituirán las reglas de autorización.

## 9.2. Flujo

```text
SEED
  ↓
NORMALIZATION
  ↓
CAPABILITY SELECTION
  ↓
CONNECTOR EXECUTION
  ↓
EVIDENCE VALIDATION
  ↓
ENTITY RESOLUTION
  ↓
GRAPH UPDATE
  ↓
ENRICHMENT PROPOSAL
  ↓
POLICY CHECK
  ↓
EXECUTION / APPROVAL / STOP
```

## 9.3. Reglas

Ejemplo:

```yaml
rule_id: authorized-domain-ct

input:
  entity_type: Domain
  verification_status:
    - VERIFIED

conditions:
  - domain_in_scope
  - passive_sources_allowed

action:
  capability: certificate_transparency_lookup

limits:
  max_depth: 3
  max_executions_per_entity: 1

priority: 20
```

## 9.4. Prevención de bucles

Obligatorio:

- Identificador único por trabajo.
- Deduplicación de investigaciones equivalentes.
- Registro de transiciones ejecutadas.
- Profundidad máxima.
- Número máximo de pivotes.
- Límite de trabajos por investigación.
- Límite temporal.
- Presupuesto máximo de consultas.
- Límite de nuevas entidades.
- Cancelación.
- Detección de ciclos.

Una investigación automática debe poder detenerse de forma determinista.

## 9.5. Priorización

Calcular la utilidad estimada de una investigación utilizando:

- Relevancia para el objetivo.
- Calidad de las evidencias disponibles.
- Coste estimado.
- Fiabilidad del proveedor.
- Novedad esperada.
- Riesgo de falsos positivos.
- Restricciones del caso.

No incrementar automáticamente la confianza por acumular resultados de fuentes dependientes.

---

# 10. GRAFO DE CONOCIMIENTO

## 10.1. Referencias

https://github.com/cytoscape/cytoscape.js

https://github.com/networkx/networkx

https://github.com/denoflore/trace

## 10.2. Funcionalidades visuales

Implementar:

- Nodos por tipo.
- Aristas por relación.
- Etiquetas.
- Iconos.
- Colores por estado.
- Búsqueda.
- Zoom.
- Filtros.
- Expansión de vecinos.
- Vista de detalle.
- Evidencias asociadas.
- Confianza de relaciones.
- Relaciones contradictorias.
- Selección múltiple.
- Exportación.

No cargar el grafo completo en el navegador si su tamaño resulta excesivo.

Implementar expansión progresiva y consultas paginadas.

## 10.3. Navegación

Al seleccionar una entidad mostrar:

- Identificador.
- Tipo.
- Atributos.
- Observaciones.
- Fuentes.
- Relaciones.
- Confianza.
- Contradicciones.
- Historial.
- Investigaciones disponibles.

## 10.4. Análisis

Implementar progresivamente:

- Camino más corto.
- Componentes conectados.
- Detección de comunidades.
- Centralidad.
- Relaciones indirectas.
- Subgrafos filtrados.

No utilizar centralidad como prueba de relevancia criminal, personal o empresarial.

### DoD

Una investigación sintética debe permitir:

1. Visualizar diez entidades relacionadas.
2. Seleccionar una entidad.
3. Consultar su evidencia.
4. Filtrar relaciones candidatas.
5. Expandir vecinos.
6. Exportar el subgrafo.
7. Recuperar la misma información al reiniciar.

---

# 11. DOCUMENTOS E IMÁGENES

## 11.1. Referencias

https://github.com/ExifTool/exiftool

https://github.com/alephdata/aleph

## 11.2. Documentos

Admitir progresivamente:

- PDF.
- DOCX.
- HTML.
- TXT.
- CSV.
- JSON.
- XLSX.

Extraer:

- Texto.
- Metadatos.
- Fechas.
- Referencias a organizaciones.
- URLs.
- Dominios.
- Referencias documentales.

Conservar:

- Archivo original, cuando proceda.
- Hash SHA-256.
- Resultado de extracción.
- Versión del extractor.
- Evidencias.
- Errores.

## 11.3. Imágenes

Implementar:

- Extracción EXIF.
- Hash criptográfico.
- Hash perceptual.
- Detección de duplicados.
- Comparación entre imágenes autorizadas.
- Extracción de texto mediante OCR.
- Identificación de procedencia documental.
- Redacción de metadatos sensibles en exportaciones.

La similitud de imágenes no demuestra identidad personal.

No construir reconocimiento biométrico masivo de personas.

## 11.4. Seguridad de archivos

- Limitar tamaño.
- Validar MIME y contenido.
- Evitar path traversal.
- Restringir recursos.
- Aislar procesamiento de archivos no confiables.
- No ejecutar macros.
- No ejecutar contenido embebido.
- Detectar archivos malformados.
- Registrar fallos.

---

# 12. MACHINE LEARNING

## 12.1. Objetivo

Permitir entrenar modelos con datos producidos y revisados por la plataforma.

El entrenamiento no debe ser obligatorio para utilizar el producto.

## 12.2. Modelos iniciales

### Modelo A: resolución de entidades

Predecir si dos registros representan probablemente la misma entidad.

Entradas:

- Similitud textual.
- Coincidencias de atributos.
- Evidencias independientes.
- Compatibilidad temporal.
- Contradicciones.

Salida:

```text
MATCH_CANDIDATE
NON_MATCH
REVIEW_REQUIRED
```

No utilizar la predicción como autorización para fusionar personas automáticamente.

### Modelo B: clasificación de documentos

Clasificar documentos en categorías relevantes.

### Modelo C: calidad de observaciones

Estimar la probabilidad de que una observación sea correcta.

### Modelo D: fiabilidad de conectores

Estimar el rendimiento esperado de proveedores por tarea y contexto.

## 12.3. Referencias

https://github.com/rapidfuzz/RapidFuzz

https://github.com/huggingface/sentence-transformers

https://github.com/networkx/networkx

## 12.4. Entrenamiento

Implementar pipeline con:

- Selección de dataset.
- Exportación.
- Anonimización cuando corresponda.
- Etiquetado.
- Validación.
- División train/validation/test.
- Entrenamiento.
- Evaluación.
- Registro de métricas.
- Registro de versiones.
- Comparación.
- Activación controlada.
- Rollback.

Evitar leakage entre conjuntos de entrenamiento y evaluación.

Cuando varias observaciones procedan de la misma entidad o fuente, diseñar particiones que eviten que duplicados relacionados contaminen los resultados.

No entrenar automáticamente con todas las observaciones sin revisión.

## 12.5. Versionado

Registrar:

```text
model_id
model_version
dataset_version
training_timestamp
features
hyperparameters
metrics
artifact_hash
deployment_status
```

## 12.6. Comparación

Debe poder compararse:

```text
Rule-based resolver
        VS
RapidFuzz resolver
        VS
ML resolver
```

Métricas:

- Precision.
- Recall.
- F1.
- False positive rate.
- Calibration.
- Latencia.
- Consumo de memoria.

La configuración de umbrales debe priorizar evitar fusiones incorrectas.

---

# 13. INTELIGENCIA GENERATIVA

Implementar como módulo opcional.

No debe formar parte del núcleo de autorización.

## 13.1. Capacidades

Un modelo generativo podrá:

- Resumir evidencias.
- Explicar relaciones.
- Proponer hipótesis.
- Sugerir nuevas investigaciones.
- Generar consultas.
- Ayudar a clasificar documentos.
- Generar borradores de informes.

## 13.2. Restricciones

Un LLM no puede:

- Inventar fuentes.
- Confirmar identidades sin evidencias.
- Modificar el alcance autorizado.
- Ejecutar herramientas arbitrarias.
- Saltarse la revisión humana.
- Cambiar las políticas de privacidad.
- Autorizar por sí mismo nuevos tratamientos de datos.

Las salidas de modelos deben ser consideradas no confiables.

Los documentos y páginas recuperados pueden contener prompt injection.

## 13.3. Integración

Priorizar una interfaz propia mediante Python.

Permitir proveedores:

- Locales.
- APIs compatibles con OpenAI.
- Otros adaptadores configurables.

No exigir MCP.

La capa LLM debe ser sustituible y opcional.

---

# 14. OBSERVABILIDAD Y RESILIENCIA

## 14.1. Panel visual

Crear una pantalla de estado de herramientas.

Columnas:

```text
Tool
Capability
Status
Last execution
Success rate
Average latency
Last error
Provider
Configuration
Actions
```

Estados visuales:

- Verde: disponible.
- Amarillo: degradado.
- Rojo: fallido.
- Gris: no instalado.
- Azul: ejecutándose.

Los colores deben acompañarse de etiquetas y elementos accesibles.

## 14.2. Métricas

Registrar:

- Ejecuciones.
- Éxitos.
- Errores.
- Timeouts.
- Latencia.
- Reintentos.
- Resultados obtenidos.
- Resultados nuevos.
- Duplicados.
- Conflictos.
- Calidad de resultados.
- Recursos utilizados.

No equiparar un número elevado de resultados con una mayor calidad.

## 14.3. Benchmark de conectores

Comparar herramientas que realizan la misma función.

Ejemplo:

```text
Subdomain discovery:

Provider A
Provider B
Provider C
```

Evaluar:

- Cobertura.
- Precisión estimada.
- Resultados exclusivos.
- Coincidencias.
- Latencia.
- Disponibilidad.
- Coste.
- Uso de recursos.

Permitir que el analista seleccione la estrategia óptima.

## 14.4. Recuperación

Diseñar pruebas de:

- Timeout.
- Error HTTP.
- API key inválida.
- Rate limiting.
- Fallo de proceso externo.
- Resultado malformado.
- Reinicio del worker.
- Reinicio de la aplicación.
- Caída temporal de base de datos.
- Cancelación manual.

Los trabajos deben tener estados persistentes.

Una caída de un proveedor nunca debe corromper el grafo.

---

# 15. API REST

Implementar endpoints versionados.

Contrato inicial:

```text
POST   /api/v1/cases
GET    /api/v1/cases
GET    /api/v1/cases/{id}

POST   /api/v1/cases/{id}/seeds
POST   /api/v1/cases/{id}/investigations

GET    /api/v1/investigations/{id}
POST   /api/v1/investigations/{id}/cancel

GET    /api/v1/connectors
GET    /api/v1/connectors/{id}/health

GET    /api/v1/entities
GET    /api/v1/entities/{id}

GET    /api/v1/graph
GET    /api/v1/graph/entities/{id}/neighbors

GET    /api/v1/evidence/{id}

GET    /api/v1/jobs/{id}

GET    /api/v1/models
POST   /api/v1/models/train

POST   /api/v1/reports
GET    /api/v1/reports/{id}
```

No todos los endpoints necesitan implementarse en la primera fase.

Pero todos los endpoints implementados deben:

- Validar entradas.
- Respetar autorización.
- Documentarse mediante OpenAPI.
- Tener respuestas tipadas.
- Utilizar errores estructurados.
- Contar con pruebas.

Añadir paginación y filtros cuando proceda.

Para trabajos largos utilizar ejecución asíncrona con identificador persistente.

---

# 16. INTERFAZ WEB

## 16.1. Pantallas

Crear progresivamente:

### Dashboard

- Investigaciones recientes.
- Estado de conectores.
- Trabajos activos.
- Resultados.
- Alertas.
- Métricas.

### Investigations

- Crear investigación.
- Definir alcance.
- Añadir seeds.
- Lanzar recolección.
- Consultar progreso.
- Cancelar trabajos.

### Graph Explorer

- Grafo interactivo.
- Búsqueda.
- Expansión.
- Filtros.
- Evidencias.
- Relaciones.

### Evidence Explorer

- Observaciones.
- Fuente.
- Fecha.
- Extractor.
- Confianza.
- Contradicciones.

### Connector Manager

- Herramientas disponibles.
- Configuración.
- Errores.
- Estadísticas.
- Pruebas de conectividad.

### Model Lab

- Datasets.
- Etiquetado.
- Entrenamientos.
- Métricas.
- Comparaciones.
- Versiones.

### Reports

- Informes.
- Exportaciones.
- Historial.
- Evidencias.

## 16.2. Requisitos UX

No bloquear la interfaz durante tareas largas.

Mostrar progreso real, no animaciones simuladas.

Diferenciar claramente:

- No encontrado.
- No consultado.
- Consulta fallida.
- Sin autorización.
- Resultado ambiguo.
- Resultado confirmado.

Una búsqueda que falla no puede presentarse como una búsqueda sin resultados.

---

# 17. SEGURIDAD

Implementar:

- Autenticación adecuada al despliegue.
- Aislamiento entre casos.
- Control de acceso por caso.
- Validación de URLs.
- Protección SSRF.
- Protección contra path traversal.
- Restricción de ejecución de subprocess.
- Gestión de secretos.
- Logs sin credenciales.
- Sanitización de contenido.
- Protección frente a inyección SQL.
- Protección frente a XSS.
- Límites de recursos.
- Retención y eliminación.
- Auditoría de acciones.
- Exportación controlada.

Los conectores no deben poder consultar arbitrariamente servicios internos, endpoints de metadatos cloud ni direcciones locales utilizando URLs controladas por fuentes externas.

Implementar defensas explícitas contra DNS rebinding y redirecciones hacia destinos prohibidos.

Las entradas recuperadas de internet deben tratarse como datos no confiables.

---

# 18. FASES DE DESARROLLO

## FASE 0 — Análisis y decisiones

### Objetivo

Establecer una arquitectura implementable.

### Tareas

1. Inspeccionar el repositorio actual.
2. Revisar dependencias.
3. Analizar proyectos de referencia.
4. Evaluar licencias.
5. Definir arquitectura.
6. Definir esquema.
7. Definir contratos.
8. Preparar backlog.

### Entregables

```text
docs/ARCHITECTURE.md
docs/DECISIONS.md
docs/REFERENCES.md
docs/ENTITY_MODEL.md
docs/CONNECTOR_SPEC.md
docs/PROJECT_STATUS.md
```

### DoD

- Arquitectura documentada.
- Dependencias justificadas.
- Referencias analizadas.
- Contratos definidos.
- Riesgos registrados.
- Plan de implementación establecido.
- Ninguna dependencia externa incompatible aceptada sin justificación.

---

## FASE 1 — Núcleo funcional

### Objetivo

Crear un MVP ejecutable con casos, observaciones, entidades y un grafo básico.

### Funcionalidades

- Backend FastAPI.
- PostgreSQL.
- Migraciones.
- Gestión de casos.
- Seeds tipadas.
- Observaciones.
- Evidencias.
- Grafo básico.
- API.
- Frontend inicial.

### Entregables

```text
backend/app/api/
backend/app/cases/
backend/app/entities/
backend/app/evidence/
backend/app/graph/
backend/migrations/
frontend/
docker-compose.yml
```

### DoD

Demostrar:

1. Arranque desde cero.
2. Creación de una investigación.
3. Inserción de una seed.
4. Importación de observaciones sintéticas.
5. Creación de entidades.
6. Visualización del grafo.
7. Consulta de evidencia.
8. Persistencia tras reinicio.
9. Ejecución de pruebas automatizadas.

No dar por terminada la fase si la interfaz solamente utiliza datos hardcodeados.

---

## FASE 2 — Conectores y recolección

### Objetivo

Ejecutar investigaciones reales mediante proveedores intercambiables.

### Implementación

Conectores iniciales:

1. DNS público.
2. Certificate Transparency.
3. RDAP.
4. Subfinder.
5. Importador JSON/CSV.
6. ExifTool para archivos proporcionados.

Implementar posteriormente Amass, theHarvester y otros adaptadores.

### Entregables

```text
backend/app/connectors/
backend/app/normalization/
backend/app/orchestration/
docs/CONNECTOR_SPEC.md
```

### DoD

- Conectores registrados.
- Healthchecks.
- Ejecución controlada.
- Normalización.
- Persistencia.
- Evidencias.
- Errores visibles.
- Fallback funcional.
- Pruebas con proveedores simulados y al menos una fuente real permitida.

Los tests CI no deben depender de la disponibilidad de servicios externos.

---

## FASE 3 — Correlación y resolución

### Objetivo

Convertir resultados aislados en conocimiento verificable.

### Implementación

- Normalización avanzada.
- Deduplicación.
- Comparación de entidades.
- Conflictos.
- Relaciones.
- Confianza.
- Revisión humana.
- Procedencia.

### Referencias

https://github.com/opensanctions/followthemoney

https://github.com/rapidfuzz/RapidFuzz

https://github.com/OpenOSINT/OpenOSINT

### Entregables

```text
backend/app/resolution/
backend/app/graph/
backend/app/evidence/
docs/ENTITY_MODEL.md
```

### DoD

- Coincidencias candidatas.
- Conflictos conservados.
- Fusiones controladas.
- Historial de decisiones.
- Evidencias asociadas a relaciones.
- Pruebas de falsos positivos.
- Reversión de fusiones.
- Ausencia de propagación automática desde coincidencias ambiguas.

---

## FASE 4 — Investigación automática

### Objetivo

Implementar un motor que seleccione nuevas investigaciones justificadas.

### Funcionalidades

- Motor de reglas.
- Scheduler.
- Cola persistente.
- Límites de profundidad.
- Políticas de alcance.
- Deduplicación de trabajos.
- Reintentos.
- Cancelación.
- Aprobación humana.
- Registro de decisiones.

### Entregables

```text
backend/app/orchestration/
backend/app/policies/
workers/
docs/INVESTIGATION_ENGINE.md
```

### DoD

Demostrar:

1. Una seed genera trabajos.
2. Los trabajos producen observaciones.
3. Las observaciones actualizan el grafo.
4. Las reglas proponen nuevas investigaciones.
5. Las políticas permiten o bloquean la ejecución.
6. No aparecen bucles infinitos.
7. Se respetan todos los presupuestos.
8. Los trabajos pendientes sobreviven a reinicios.

---

## FASE 5 — Análisis documental e imágenes

### Objetivo

Incorporar documentos y archivos autorizados.

### Referencias

https://github.com/ExifTool/exiftool

https://github.com/alephdata/aleph

### Entregables

```text
backend/app/connectors/documents/
backend/app/connectors/images/
backend/app/evidence/
docs/DOCUMENT_PROCESSING.md
```

### DoD

- Importación de archivos.
- Validación.
- Extracción.
- Hash.
- Metadatos.
- Entidades documentales.
- Referencias.
- Visualización.
- Tratamiento de errores.
- Pruebas con archivos malformados.
- Protección contra ejecución de contenido.

---

## FASE 6 — Machine learning

### Objetivo

Introducir modelos entrenables y evaluables.

### Implementación

- Datasets etiquetados.
- Entrenamiento.
- Evaluación.
- Comparación.
- Versionado.
- Inferencia.
- Rollback.

### Referencias

https://github.com/rapidfuzz/RapidFuzz

https://github.com/huggingface/sentence-transformers

### Entregables

```text
backend/app/models/
backend/app/analytics/
models/
docs/MODEL_TRAINING.md
```

### DoD

- Dataset sintético reproducible.
- Baseline determinista.
- Modelo entrenado.
- Evaluación reproducible.
- Métricas calculadas.
- Ausencia de leakage conocido.
- Registro del experimento.
- Comparación con baseline.
- Rollback funcional.
- Ninguna fusión automática de personas basada exclusivamente en predicciones.

---

## FASE 7 — Observabilidad y resiliencia

### Objetivo

Convertir el sistema en una plataforma operativamente fiable.

### Implementación

- Dashboard de conectores.
- Métricas.
- Healthchecks.
- Circuit breakers.
- Benchmark.
- Comparación de proveedores.
- Alertas.
- Recuperación.

### Entregables

```text
backend/app/monitoring/
frontend/src/connectors/
docs/OPERATIONS.md
docs/TEST_REPORT.md
```

### DoD

Simular y verificar:

- Timeout.
- Fallo de proveedor.
- Respuesta malformada.
- Rate limiting.
- API no configurada.
- Reinicio de worker.
- Fallback.
- Recuperación.

Todas las situaciones deben tener resultado observable y registrado.

---

## FASE 8 — IA generativa e informes

### Objetivo

Introducir asistencia inteligente sin perder trazabilidad.

### Funcionalidades

- Resumen de evidencias.
- Explicación de relaciones.
- Propuestas de investigación.
- Generación de informes.
- Exportación JSON.
- Exportación CSV.
- Exportación GraphML.
- Informe HTML o PDF.

### Entregables

```text
backend/app/reporting/
backend/app/models/
frontend/src/pages/
docs/AI_INTEGRATION.md
```

### DoD

- Informe basado exclusivamente en evidencias almacenadas.
- Referencias verificables.
- Dudas y contradicciones visibles.
- Ausencia de fuentes inventadas.
- Funcionamiento sin proveedor LLM.
- Pruebas de prompt injection.
- Exportaciones reproducibles.

---

## FASE 9 — Endurecimiento y entrega

### Objetivo

Preparar una versión estable y reproducible.

### Tareas

- Revisar arquitectura.
- Eliminar código muerto.
- Corregir errores.
- Ejecutar pruebas.
- Analizar dependencias.
- Revisar seguridad.
- Validar documentación.
- Verificar instalación limpia.
- Comprobar rendimiento.
- Preparar demo.

### Entregables

```text
README.md
docs/ARCHITECTURE.md
docs/SECURITY.md
docs/OPERATIONS.md
docs/TEST_REPORT.md
docs/PROJECT_STATUS.md
docs/HANDOFF.md
```

### DoD

- Instalación reproducible.
- Tests satisfactorios.
- Migraciones correctas.
- API documentada.
- Frontend funcional.
- Datos de demostración reproducibles.
- Errores controlados.
- Sin credenciales hardcodeadas.
- Sin dependencias obligatorias de pago.
- Sin funcionalidades falsas presentadas como completas.

---

# 19. CONTRATO DE FINALIZACIÓN POR FASE

Cada fase debe generar un informe de finalización.

Formato obligatorio:

```yaml
phase: 3
name: entity_resolution

status: COMPLETED

scope:
  planned:
    - candidate_matching
    - contradiction_handling
    - analyst_review

  delivered:
    - candidate_matching
    - contradiction_handling
    - analyst_review

artifacts:
  - path: backend/app/resolution/
    exists: true

  - path: docs/ENTITY_MODEL.md
    exists: true

tests:
  executed: true
  total: 42
  passed: 42
  failed: 0
  skipped: 0

acceptance:
  criteria_total: 8
  criteria_passed: 8

limitations: []

known_issues: []

evidence:
  - test_report_reference
  - execution_log_reference

next_phase_ready: true
```

Los valores numéricos son un ejemplo, no resultados reales.

## Estados permitidos

```text
NOT_STARTED
IN_PROGRESS
BLOCKED
PARTIALLY_COMPLETED
COMPLETED
FAILED
```

## Reglas

Una fase solamente puede marcarse `COMPLETED` si:

1. Todos sus entregables existen.
2. Sus pruebas obligatorias se han ejecutado.
3. Todos los criterios de aceptación se cumplen.
4. No quedan fallos bloqueantes.
5. La documentación coincide con el código.
6. Existe evidencia verificable de funcionamiento.

Una funcionalidad no se considera implementada porque exista una clase vacía, endpoint simulado, comentario TODO o mock.

Los mocks son válidos para pruebas, pero deben identificarse claramente.

Si un criterio no puede verificarse, el estado no puede ser `COMPLETED`.

Si una dependencia externa impide una prueba real, registrar el bloqueo y mantener las pruebas deterministas correspondientes.

---

# 20. CALIDAD Y TESTING

## 20.1. Estrategia

Implementar:

- Unit tests.
- Integration tests.
- Contract tests.
- End-to-end tests.
- Security tests.
- Failure injection tests.
- Regression tests.

## 20.2. Casos críticos

Probar expresamente:

### Identidades

Dos personas comparten nombre.

Resultado esperado: entidades separadas.

### Fuentes contradictorias

Dos registros ofrecen atributos incompatibles.

Resultado esperado: conservar ambas afirmaciones.

### Fallback

Una herramienta falla.

Resultado esperado: ejecutar proveedor alternativo permitido.

### Persistencia

Reiniciar servidor.

Resultado esperado: recuperar investigaciones y trabajos.

### Duplicación

Importar dos veces el mismo resultado.

Resultado esperado: evitar duplicados semánticos sin eliminar evidencias.

### Límites

Una investigación produce múltiples rutas de expansión.

Resultado esperado: respetar límites de profundidad, consultas y tiempo.

### Seguridad

Una fuente devuelve una URL hacia un servicio interno.

Resultado esperado: bloquear el acceso.

### IA

Un documento contiene instrucciones dirigidas al agente.

Resultado esperado: tratar las instrucciones como contenido no confiable.

### Privacidad

Se intenta procesar un dato excluido por la política.

Resultado esperado: impedir su incorporación ordinaria al grafo.

---

# 21. DATOS DE DEMOSTRACIÓN

Crear un dataset completamente sintético.

Debe incluir:

- Empresas ficticias.
- Personas ficticias.
- Usuarios ficticios.
- Dominios reservados para ejemplos.
- Documentos de prueba.
- Relaciones válidas.
- Coincidencias ambiguas.
- Contradicciones.
- Fuentes duplicadas.
- Observaciones caducadas.
- Proveedores fallidos simulados.

Debe permitir demostrar todo el funcionamiento sin depender de datos personales reales.

Los datos sintéticos deben identificarse visualmente como tales.

---

# 22. DOCUMENTACIÓN DE ESTADO

Mantener actualizados los siguientes documentos.

## PROJECT_STATUS.md

Debe incluir:

```text
Current phase
Current task
Completed tasks
Pending tasks
Blocked tasks
Known problems
Last verified tests
Next recommended action
```

## HANDOFF.md

Debe permitir que otro agente continúe el trabajo.

Debe incluir:

```text
Architecture summary
Current state
Recent modifications
Important decisions
How to start
How to test
Known issues
Next task
```

## DECISIONS.md

Registrar decisiones arquitectónicas y sus alternativas.

## REFERENCES.md

Registrar los repositorios inspeccionados y su uso real.

## TEST_REPORT.md

Registrar comandos ejecutados, resultados y limitaciones.

---

# 23. CI/CD

Configurar GitHub Actions para:

- Lint.
- Type checking.
- Unit tests.
- Integration tests.
- Frontend build.
- Security checks.
- Dependency review.

No utilizar servicios OSINT reales en pruebas CI estándar.

Utilizar fixtures deterministas.

Los tests que requieren API keys deben ejecutarse únicamente en workflows autorizados.

---

# 24. CRITERIOS GLOBALES DE ACEPTACIÓN

El producto final debe permitir este escenario:

1. Crear una investigación autorizada de una empresa ficticia.
2. Introducir su dominio.
3. Ejecutar varias fuentes OSINT.
4. Obtener observaciones normalizadas.
5. Guardar procedencia.
6. Correlacionar resultados.
7. Construir un grafo.
8. Detectar relaciones.
9. Mostrar contradicciones.
10. Sugerir nuevas investigaciones.
11. Ejecutar las autorizadas.
12. Detener las no permitidas.
13. Recuperarse del fallo de una herramienta.
14. Mostrar errores en la interfaz.
15. Consultar evidencias.
16. Exportar resultados.
17. Entrenar un modelo con datos sintéticos etiquetados.
18. Comparar su resultado con el baseline.
19. Generar un informe.
20. Recuperar toda la investigación tras reiniciar.

No se considera finalizado el proyecto si cualquiera de las capacidades obligatorias se encuentra únicamente simulada.

Las funcionalidades externas opcionales pueden permanecer deshabilitadas por falta de credenciales o licencias, siempre que se documenten y el sistema continúe funcionando.

---

# 25. INSTRUCCIONES DE EJECUCIÓN PARA EL AGENTE

Trabaja de forma autónoma.

Orden de ejecución:

1. Inspecciona el repositorio.
2. Analiza las referencias necesarias.
3. Diseña la arquitectura.
4. Documenta decisiones.
5. Implementa la fase actual.
6. Escribe y ejecuta pruebas.
7. Corrige errores.
8. Verifica los criterios DoD.
9. Actualiza documentación.
10. Registra el contrato de finalización.
11. Continúa con la siguiente fase.

No avances si faltan elementos críticos de la fase anterior.

Prioriza entregar módulos verticalmente funcionales sobre crear todas las capas de forma superficial.

Una entrega vertical debe conectar:

```text
UI → API → Service → Persistence → Tests
```

Y, cuando corresponda:

```text
UI → Investigation → Connector → Observation
   → Evidence → Entity → Graph
```

## Prohibiciones

No:

- Declarar éxito sin ejecutar pruebas.
- Inventar resultados.
- Ocultar errores.
- Presentar mocks como implementaciones finales.
- Introducir dependencias externas sin revisar licencias.
- Introducir servicios de pago como requisitos obligatorios.
- Añadir complejidad sin justificación.
- Eliminar evidencias contradictorias.
- Confirmar identidades basándose solamente en similitud.
- Ejecutar conectores fuera del alcance autorizado.
- Permitir que un LLM omita políticas.
- Terminar una fase dejando documentación obsoleta.

## Criterio de priorización

Ante dos implementaciones equivalentes, elegir aquella que:

1. Mantenga los requisitos funcionales.
2. Sea más sencilla.
3. Tenga menos dependencias.
4. Sea más fácil de probar.
5. Sea más fácil de sustituir.
6. Tenga mejor trazabilidad.
7. Consuma menos recursos.

---

# 26. PRIMERA ACCIÓN

Comienza inmediatamente por la FASE 0.

Inspecciona el repositorio disponible.

Si no existe una implementación previa, inicializa el proyecto.

Evalúa las referencias correspondientes al núcleo.

Entrega:

- Arquitectura propuesta.
- Modelo de datos.
- Contratos iniciales.
- Decisiones tecnológicas.
- Estructura del repositorio.
- Plan de ejecución.
- Matriz de funcionalidades y fases.
- Riesgos.
- Definition of Done de la fase 0.

Después, si se cumplen los criterios, inicia la FASE 1.

El objetivo es construir progresivamente un producto funcional y verificable, no limitarse a generar documentación.