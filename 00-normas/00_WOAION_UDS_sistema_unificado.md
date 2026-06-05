---
uid: GLB_GOV_000_sistema_unificado
titulo: "WOAION UDS — Sistema de Documentación Unificado"
ambito: GLB
categoria: GOV
estado: certified
fecha_creacion: 2026-05-31
version: 1.0.0
version_estandar: "4.0"
autor: WOAION Core
licencia: CC-BY-SA 4.0
publico: true
idioma: es
---

# WOAION UDS — Sistema de Documentación Unificado
### Versión 4.0 · Estándar Global

> **Propósito:** Definir la arquitectura documental única que rige toda la información producida dentro del ecosistema WOAION, tanto para uso interno como para la comunidad abierta.
>
> **Alcance:** Vault interno · Repositorios de ingeniería · Documentación pública · Contribuciones de la comunidad

---

## Por qué existe este documento

WOAION creció en dos direcciones al mismo tiempo: un sistema de gestión de conocimiento interno (Obsidian, v3.0) y un sistema de documentación técnica de ingeniería (SDT-GCI). Ambos son válidos. El problema es que operaron en paralelo sin un puente explícito.

Este documento establece la **arquitectura de cuatro capas** que unifica ambos sistemas sin eliminar ninguno, agrega la capa de comunidad abierta que faltaba, y define cómo se comunican entre sí.

---

## Índice

1. [Arquitectura de capas](#1-arquitectura-de-capas)
2. [Dominio de cada sistema de identificación](#2-dominio-de-cada-sistema-de-identificación)
3. [Esquema YAML unificado v4.0](#3-esquema-yaml-unificado-v40)
4. [Taxonomía completa de ámbitos y categorías](#4-taxonomía-completa-de-ámbitos-y-categorías)
5. [Estados documentales unificados](#5-estados-documentales-unificados)
6. [Nomenclatura y convenciones de nombre de archivo](#6-nomenclatura-y-convenciones-de-nombre-de-archivo)
7. [Trazabilidad entre capas](#7-trazabilidad-entre-capas)
8. [Arquitectura de repositorios públicos](#8-arquitectura-de-repositorios-públicos)
9. [Flujo de contribución comunitaria](#9-flujo-de-contribución-comunitaria)
10. [Control documental y versionado](#10-control-documental-y-versionado)
11. [Templates disponibles](#11-templates-disponibles)
12. [Glosario](#12-glosario)

---

## 1. Arquitectura de capas

El sistema UDS organiza toda la información en cuatro capas. Cada capa tiene su propio sistema de identificación, repositorio y audiencia, pero comparten el mismo esquema de metadatos y el mismo vocabulario controlado.

```
┌─────────────────────────────────────────────────────────────────┐
│  CAPA 0 — GOBERNANZA  (GLB)                                     │
│  Normas · Matrices · Esquemas · Este documento                  │
│  Repositorio: woaion/governance  ·  Público                     │
├─────────────────────────────────────────────────────────────────┤
│  CAPA 1 — CONOCIMIENTO  (OPE / KNW)                             │
│  Investigación · Decisiones · Bitácora · Aprendizajes           │
│  Repositorio: vault interno Obsidian  ·  Parcialmente público   │
├─────────────────────────────────────────────────────────────────┤
│  CAPA 2 — INGENIERÍA  (PRY)                                     │
│  Planos · CAD · BOM · Cálculos · Simulaciones                   │
│  Repositorio: woaion/[proyecto]  ·  Público (open source)       │
├─────────────────────────────────────────────────────────────────┤
│  CAPA 3 — COMUNIDAD  (COM)                                      │
│  Tutoriales · Guías · Onboarding · Wiki pública                 │
│  Repositorio: woaion/docs  ·  Público                           │
└─────────────────────────────────────────────────────────────────┘
```

### Relaciones entre capas

```
Capa 0 (Gobernanza)
    ↓ define las reglas de
Capa 1 (Conocimiento)  ←──referencia──→  Capa 2 (Ingeniería)
    ↓ genera contenido para                     ↓ genera contenido para
Capa 3 (Comunidad) ←──────────────────────────┘
```

**Principio clave:** La información fluye *hacia abajo* (las normas definen todo lo demás) y *hacia la capa 3* (el conocimiento y los artefactos de ingeniería alimentan la documentación pública). Nunca en sentido inverso: una contribución comunitaria no modifica directamente un estándar; pasa por revisión interna primero.

---

## 2. Dominio de cada sistema de identificación

Uno de los puntos de confusión del sistema anterior era tener dos formatos de UID sin definir cuándo usar cuál. La respuesta es simple: **no compiten porque identifican cosas distintas**.

### UID de documento (Capa 0, 1, 3)

```
AAAAMMDD_AMB_CAT_NNN_nombre_descriptivo
```

Se usa para: notas, guías, tutoriales, decisiones, análisis, plantillas, normas, actas. Cualquier **documento** que sea principalmente texto y tenga un ciclo de vida editorial.

Ejemplos:
- `20260531_GLB_GOV_001_sistema_unificado.md`
- `20260315_OPE_DEC_007_material_bastidor.md`
- `20260401_COM_TUT_003_como_contribuir.md`

### Código de artefacto de ingeniería (Capa 2)

```
[SIGLA]-[SS]-[TIPO]-[NNN]
```

Se usa para: planos, modelos CAD, BOM, cálculos, simulaciones, especificaciones técnicas. Cualquier **artefacto** que sea referenciado por piezas, procesos de fabricación o sistemas físicos.

Ejemplos:
- `J5C-CHR-EST-001` — Plano estructural del chasis del J5 Cargo
- `SCR-SUS-CAL-003` — Cálculo de suspensión del Scrab

### Regla de coexistencia

Un documento puede **referenciar** un artefacto de ingeniería en su frontmatter. Un artefacto puede tener un documento asociado que explica sus decisiones de diseño. El UID de documento y el código de artefacto son ortogonales, no redundantes.

```yaml
# Ejemplo: documento de decisión que referencia artefactos de ingeniería
uid: 20260315_OPE_DEC_007_material_bastidor
artefactos_relacionados:
  - J5C-CHR-EST-001   # Plano que implementa esta decisión
  - J5C-CHR-BOM-001   # BOM afectada
```

---

## 3. Esquema YAML unificado v4.0

Este esquema es el único válido a partir de v4.0. Reemplaza y es compatible con el schema v3.0.

### Campos obligatorios (todos los documentos)

```yaml
---
uid: "AAAAMMDD_AMB_CAT_NNN_nombre"   # Identificador único global
titulo: "Título completo del documento"
ambito: GLB                           # GLB | OPE | PRY | COM
categoria: GOV                        # Ver sección 4
estado: ia_draft                      # Ver sección 5
fecha_creacion: 2026-05-31            # ISO 8601
version: 1.0.0                        # Semántico MAJOR.MINOR.PATCH
version_estandar: "4.0"               # Versión de este estándar
autor: "Nombre o handle"
---
```

### Campos obligatorios según ámbito

```yaml
# Si ambito: PRY
proyecto: J5C                         # Sigla del proyecto
proyecto_nombre: "JS Cargo"           # Nombre completo

# Si ambito: COM
idioma: es                            # ISO 639-1
licencia: CC-BY-SA 4.0               # SPDX identifier
```

### Campos opcionales de trazabilidad

```yaml
depende_de:
  - "20260301_OPE_ANA_001_xxx"       # UID de documento
  - "J5C-CHR-EST-001"                # Código de artefacto (ambas formas válidas)

referenciado_por:
  - "20260401_COM_TUT_001_xxx"

artefactos_relacionados:
  - J5C-CHR-EST-001
  - J5C-CHR-BOM-001

reemplaza: "20260101_OPE_DIR_001_xxx"  # Si este doc supera a otro
traduccion_de: "20260531_GLB_GOV_001_unified_docs_en"  # Si es traducción
```

### Campos opcionales de clasificación

```yaml
tags:
  - estandar
  - nomenclatura
  - v4

publico: true                          # default: false para OPE, true para COM/GLB
contribuidores:
  - "handle1"
  - "handle2"

revision_requerida: false             # Si necesita revisión periódica
proxima_revision: 2026-11-31          # Fecha de próxima revisión obligatoria
```

### Ejemplo completo

```yaml
---
uid: 20260315_PRY_DEC_007_material_bastidor_j5c
titulo: "DEC-007 — Selección de material para bastidor J5 Cargo"
ambito: PRY
categoria: DEC
estado: certified
fecha_creacion: 2026-03-15
version: 1.1.0
version_estandar: "4.0"
autor: Antigravity
proyecto: J5C
proyecto_nombre: "JS Cargo"
depende_de:
  - J5C-CHR-SIM-003
  - 20260210_PRY_ANA_002_analisis_materiales
artefactos_relacionados:
  - J5C-CHR-EST-001
publico: true
tags:
  - materiales
  - chasis
  - decision
licencia: CC-BY-SA 4.0
---
```

---

## 4. Taxonomía completa de ámbitos y categorías

### 4.1 Ámbitos (AMB)

| AMB | Nombre | Alcance | Público por defecto |
|-----|--------|---------|---------------------|
| `GLB` | Global | Normas y activos que rigen toda la bóveda | Sí |
| `OPE` | Operativo | Procesos, tareas y decisiones del día a día | No |
| `PRY` | Proyecto | Contenido específico de un proyecto | Parcial |
| `COM` | Comunidad | Documentación orientada a colaboradores externos | Sí |

### 4.2 Categorías (CAT)

#### Categorías de Gobernanza y Sistema

| CAT | Nombre | AMB Compatibles | Descripción |
|-----|--------|-----------------|-------------|
| `GOV` | Gobernanza | GLB | Normas maestras del sistema documental |
| `DIR` | Directrices | GLB, OPE | Reglas de operación y proceso |
| `MET` | Metadatos | GLB | Esquemas YAML y parámetros |
| `MAT` | Matrices | GLB | Catálogos controlados (códigos, siglas) |
| `PLT` | Plantillas | GLB, OPE | Formatos base para nuevas notas |

#### Categorías de Conocimiento y Proceso

| CAT | Nombre | AMB Compatibles | Descripción |
|-----|--------|-----------------|-------------|
| `DEC` | Decisión | OPE, PRY | Registros de decisiones de diseño |
| `ANA` | Análisis | GLB, OPE, PRY | Auditorías, análisis, estudios |
| `LOG` | Bitácora | OPE, PRY | Diario de desarrollo, entradas con fecha |
| `HIS` | Historial | GLB | Cronologías, hitos y trazabilidad |
| `REF` | Referencia | GLB, OPE, PRY | Documentos de referencia e investigación |

#### Categorías de Ingeniería y Producto

| CAT | Nombre | AMB Compatibles | Descripción |
|-----|--------|-----------------|-------------|
| `PRO` | Producto | PRY | Especificaciones de hardware/software |
| `INV` | Inventario | OPE, PRY | BOM, listado de materiales/componentes |
| `SIM` | Simulación | PRY | Documentos de análisis y simulación |
| `MFG` | Manufactura | PRY | Procesos y documentos de fabricación |
| `CAL` | Cálculo | PRY | Memorias de cálculo estructural/técnico |

#### Categorías de Comunidad y Comunicación

| CAT | Nombre | AMB Compatibles | Descripción |
|-----|--------|-----------------|-------------|
| `TUT` | Tutorial | COM, GLB | Guías paso a paso para colaboradores |
| `CON` | Contribución | COM | Pautas y flujos de contribución |
| `VIS` | Identidad Visual | GLB | Activos maestros (logos, paletas) |
| `ACT` | Acta | OPE | Registros de reuniones y decisiones grupales |

---

## 5. Estados documentales unificados

Este esquema unifica los estados que existían por separado en el vault y en el sistema de ingeniería.

### Estados de ciclo de vida editorial

| Estado | Código | Descripción | Referenciable |
|--------|--------|-------------|---------------|
| Borrador IA | `ia_draft` | Generado por IA, sin revisión humana | No |
| Borrador | `draft` | En edición activa | No |
| En revisión | `in_review` | Esperando validación interna | No |
| Revisado | `human_reviewed` | Revisado por humano, listo para certificar | Sí (con nota) |
| Certificado | `certified` | Válido para uso y referencia | Sí |
| Archivado | `archived` | Superado, solo consulta histórica | No |

### Estados de artefactos de ingeniería (Capa 2)

| Estado | Código | Descripción |
|--------|--------|-------------|
| Conceptual | `conceptual` | Exploración, no citar en diseño |
| Prototipo | `prototype` | Guía para fabricación de prototipo |
| Activo | `active` | En uso, no necesariamente validado |
| Validado | `validated` | Verificado por prueba o cálculo |
| Fabricación | `production` | Listo para producción directa |
| Archivado | `archived` | No usar, solo consulta |

### Matriz de transiciones permitidas

```
ia_draft → draft → in_review → human_reviewed → certified → archived
                                                              ↑
                                                   (cualquier estado puede archivar)
```

Para artefactos de ingeniería:
```
conceptual → prototype → active → validated → production → archived
```

---

## 6. Nomenclatura y convenciones de nombre de archivo

### 6.1 Documentos (todas las capas excepto Capa 2)

```
AAAAMMDD_AMB_CAT_NNN_nombre_descriptivo.ext
```

**Reglas:**
1. Fecha en ISO 8601 sin separadores: `20260531`
2. `AMB` y `CAT` en mayúsculas: `GLB`, `GOV`
3. `NNN` es secuencia numérica dentro de la misma `AMB+CAT+fecha` (reinicia por día o es global por categoría, según el registro de matrices)
4. `nombre_descriptivo` en `snake_case` minúsculas, sin acentos, máx. 40 caracteres
5. Extensión preferida para documentos: `.md`

**Ejemplos válidos:**
```
20260531_GLB_GOV_001_sistema_unificado.md
20260315_PRY_DEC_007_material_bastidor_j5c.md
20260401_COM_TUT_001_como_contribuir.md
20260120_OPE_LOG_045_prueba_suspension.md
```

### 6.2 Artefactos de ingeniería (Capa 2)

```
[SIGLA]-[SS]-[TIPO]-[NNN]
```

Ver SDT-GCI sección 1 para la tabla completa de tipos. Resumen de tipos más usados:

| Código | Tipo de artefacto |
|--------|-------------------|
| `EST` | Estructural (plano, diseño) |
| `MEC` | Mecánico |
| `ELC` | Eléctrico / Electrónico |
| `MFG` | Manufactura (proceso, instrucción) |
| `SIM` | Simulación |
| `DEC` | Decisión de diseño |
| `BOM` | Lista de materiales |
| `REF` | Referencia / Investigación |
| `CAL` | Cálculo |
| `SFW` | Software / Control |

### 6.3 Convenciones adicionales para archivos públicos

Los archivos destinados a la documentación pública (Capa 3) siguen las mismas reglas de nomenclatura pero añaden el prefijo de idioma cuando existen versiones en múltiples idiomas:

```
20260401_COM_TUT_001_como_contribuir.es.md
20260401_COM_TUT_001_how_to_contribute.en.md
```

---

## 7. Trazabilidad entre capas

La trazabilidad es el mecanismo que responde: **si cambio X, ¿qué más se ve afectado?**

### 7.1 Registro en frontmatter

Todo documento debe declarar sus dependencias en el frontmatter usando los campos `depende_de` y `referenciado_por`. Se aceptan UIDs de documento, códigos de artefacto, y referencias externas (URLs).

```yaml
depende_de:
  - "20260210_PRY_ANA_001_estudio_terreno"     # Documento del que depende
  - "J5C-SUS-CAL-001"                           # Artefacto del que depende

referenciado_por:
  - "20260401_COM_TUT_002_construir_suspension" # Documento que me referencia
  - "J5C-SUS-MFG-001"                           # Artefacto que me referencia
```

### 7.2 Mapa de trazabilidad entre capas (ejemplo)

```
CAPA 1 (Conocimiento)
  20260210_PRY_ANA_001_estudio_terreno_j5c
       ↓ genera datos para
  20260215_PRY_DEC_003_tipo_suspension
       ↓ documenta la decisión que implementa
CAPA 2 (Ingeniería)
  J5C-SUS-CAL-001  (Cálculo de suspensión)
       ↓ valida geometría en
  J5C-SUS-EST-002  (Plano de brazo de suspensión)
       ↓ instruye fabricación en
  J5C-SUS-MFG-001  (Proceso de fabricación)
       ↓ se resume para
CAPA 3 (Comunidad)
  20260401_COM_TUT_004_suspension_j5c
```

### 7.3 Reglas de trazabilidad

1. **No romper hacia arriba:** Un documento de Capa 3 no puede modificar un artefacto de Capa 2. Solo puede referenciar.
2. **Declarar al crear:** El campo `depende_de` se llena en el momento de creación del documento, no después.
3. **Actualizar al modificar:** Cuando se archiva un documento, todos los que lo referencian deben actualizarse o indicarse en el CHANGELOG del proyecto.

---

## 8. Arquitectura de repositorios públicos

### 8.1 Estructura de repositorios

```
GitHub: woaion/
├── governance/               ← Este repositorio (Capa 0)
│   ├── README.md
│   ├── 00-normas/
│   ├── 01-matrices/
│   ├── 02-plantillas/
│   └── 03-ejemplos/
│
├── docs/                     ← Documentación pública (Capa 3)
│   ├── README.md
│   ├── getting-started/
│   ├── standards/            ← Versión pública de las normas
│   ├── contribute/
│   ├── projects/
│   │   ├── j5-cargo/
│   │   ├── scrab/
│   │   └── jsx-bot/
│   └── reference/
│
├── j5-cargo/                 ← Proyecto J5 Cargo (Capa 2)
│   ├── README.md
│   ├── CHANGELOG.md
│   ├── docs/
│   ├── planos/
│   ├── modelos_3d/
│   ├── manufactura/
│   ├── simulaciones/
│   └── [estructura SDT-GCI completa]
│
├── scrab/                    ← Proyecto Scrab (Capa 2)
│
└── jsx-bot/                  ← Proyecto JSX Bot (Capa 2)
```

### 8.2 Archivos raíz obligatorios en cada repositorio

| Archivo | Propósito |
|---------|-----------|
| `README.md` | Descripción, estado, cómo empezar |
| `CHANGELOG.md` | Historial de cambios semánticos |
| `CONTRIBUTING.md` | Guía de contribución comunitaria |
| `LICENSE` | Licencia del proyecto |
| `CODE_OF_CONDUCT.md` | Código de conducta de la comunidad |

---

## 9. Flujo de contribución comunitaria

### 9.1 Para un nuevo colaborador

```
1. Leer README del repositorio relevante
       ↓
2. Leer CONTRIBUTING.md
       ↓
3. Consultar 00_WOAION_UDS_sistema_unificado.md (este doc)
       ↓
4. Consultar 01_REGISTRO_CATEGORIAS.md para códigos
       ↓
5. Seleccionar la plantilla adecuada (ver sección 11)
       ↓
6. Crear documento con UID correcto, estado: ia_draft o draft
       ↓
7. Registrar cualquier código nuevo en matrices ANTES de usarlo
       ↓
8. Abrir Pull Request con descripción clara
       ↓
9. Revisión interna → estado: human_reviewed
       ↓
10. Merge → estado: certified (o el que corresponda)
```

### 9.2 Tipos de contribución aceptadas

| Tipo | Template a usar | Estado inicial |
|------|-----------------|----------------|
| Corrección en doc existente | — (editar archivo) | Mantener estado |
| Nueva guía/tutorial | `PLT_tutorial_comunidad` | `draft` |
| Nueva decisión de diseño | `PLT_decision_diseno` | `draft` |
| Nuevo artefacto de ingeniería | `PLT_artefacto_ingenieria` | `conceptual` |
| Traducción | `PLT_traduccion` | `draft` |
| Reporte de problema | Issue en GitHub | — |

### 9.3 Qué NO se puede contribuir directamente

- Modificar normas GLB o GOV (requiere proceso de RFC interno)
- Cambiar el estado de un documento a `certified` (solo maintainers)
- Crear nuevos códigos AMB o categorías GOV (requiere proceso de RFC)
- Modificar matrices GLB (solo maintainers con RFC aprobado)

---

## 10. Control documental y versionado

### 10.1 Versionado semántico para documentos

```
v[MAJOR].[MINOR].[PATCH]
```

| Nivel | Cuándo | Ejemplo |
|-------|--------|---------|
| `MAJOR` | Cambio conceptual completo, incompatible con versión anterior | `1.0.0 → 2.0.0` |
| `MINOR` | Nueva sección, cambio de contenido significativo | `1.0.0 → 1.1.0` |
| `PATCH` | Corrección de errores, ajustes menores | `1.0.0 → 1.0.1` |

### 10.2 Versionado de artefactos de ingeniería

Para artefactos de Capa 2, se usa la combinación:
```
v[MAJOR].[MINOR]-R[NN]
```
Donde `R[NN]` es el número de revisión del plano/archivo CAD.

### 10.3 CHANGELOG obligatorio

Cada repositorio mantiene un `CHANGELOG.md` con el formato:

```markdown
## [v1.2.0] — 2026-05-31

### Agregado
- Nueva sección de trazabilidad entre capas

### Cambiado
- Schema YAML: campo `estado_verificacion` reemplazado por `estado`

### Corregido
- Descripción incorrecta de categoría COM

### Archivado
- 20260101_OPE_DIR_001 → reemplazado por este documento
```

---

## 11. Templates disponibles

Los siguientes templates están disponibles en `governance/02-plantillas/`. Cada uno implementa el schema v4.0 para su caso de uso.

| Archivo | Uso |
|---------|-----|
| `PLT_documento_base.md` | Punto de partida para cualquier documento |
| `PLT_decision_diseno.md` | Registro de decisión de diseño (DEC) |
| `PLT_artefacto_ingenieria.md` | Cabecera para artefacto de Capa 2 |
| `PLT_tutorial_comunidad.md` | Tutorial para colaboradores (COM) |
| `PLT_bitacora_entrada.md` | Entrada de bitácora de desarrollo (LOG) |
| `PLT_acta_reunion.md` | Acta de reunión (ACT) |
| `PLT_bom_proyecto.md` | Lista de materiales (BOM/INV) |

---

## 12. Glosario

| Término | Definición |
|---------|------------|
| **UDS** | Unified Documentation System — este sistema |
| **UID** | Identificador único de documento en formato `AAAAMMDD_AMB_CAT_NNN_nombre` |
| **Código de artefacto** | Identificador de artefacto de ingeniería en formato `SIGLA-SS-TIPO-NNN` |
| **Capa** | Nivel de abstracción del sistema documental (0–3) |
| **Ámbito (AMB)** | Alcance de autoridad de un documento (GLB, OPE, PRY, COM) |
| **Categoría (CAT)** | Tipo funcional de un documento dentro de su ámbito |
| **Estado** | Fase del ciclo de vida de un documento |
| **Trazabilidad** | Capacidad de seguir la cadena de dependencias entre documentos y artefactos |
| **Vault** | Repositorio de notas en Obsidian, corresponde principalmente a Capas 0 y 1 |
| **BOM** | Bill of Materials — lista de componentes con cantidades y referencias |
| **DEC** | Categoría de registro de decisión de diseño |
| **RFC** | Request for Change — proceso para modificar normas GLB |
| **SDT-GCI** | Sistema de Documentación Técnica de Gestión de Conocimiento de Ingeniería (documento de referencia de Capa 2) |
| **ISE** | Índice de Simbiosis Ecológica — métrica interna de WOAION, v0.2 |

---

## Historial de versiones

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 4.0.0 | 2026-05-31 | Versión inicial del UDS. Unifica schema v3.0 (vault) con SDT-GCI (ingeniería). Agrega Capa COM y AMB COM. |

---

*WOAION UDS · v4.0.0 · Licencia CC-BY-SA 4.0*
*Este documento es la fuente de verdad para el sistema documental de WOAION.*
