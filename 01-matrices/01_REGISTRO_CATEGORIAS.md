---
uid: 20260531_GLB_MAT_001_registro_categorias
titulo: "Registro Maestro de Ámbitos y Categorías"
ambito: GLB
categoria: MAT
estado: certified
fecha_creacion: 2026-03-14
fecha_actualizacion: 2026-05-31
version: 2.0.0
version_estandar: "4.0"
autor: Archivista
reemplaza: 01_REGISTRO_CATEGORIAS
publico: true
depende_de:
  - 20260531_GLB_GOV_000_sistema_unificado
tags:
  - matriz
  - ambitos
  - categorias
  - vocabulario_controlado
---

# Registro Maestro de Ámbitos y Categorías

> Este documento es el **vocabulario controlado** del sistema WOAION UDS. Ningún código de Ámbito (`AMB`) ni de Categoría (`CAT`) puede usarse en un documento si no está registrado aquí primero.
>
> Para proponer un código nuevo, abrir un issue con el prefijo `[MATRIZ]` antes de usarlo.

---

## 1. Ámbitos (AMB)

Los ámbitos definen el alcance de autoridad de un documento: a quién aplica y desde qué nivel del sistema habla.

| AMB | Nombre | Alcance | Público por defecto | Notas |
| :--- | :--- | :--- | :---: | :--- |
| **GLB** | Global | Normas y activos que rigen toda la bóveda y todos los proyectos. | ✅ | Mayor nivel de autoridad. Cambios requieren RFC. |
| **OPE** | Operativo | Procesos, tareas y directrices del día a día (Zona 1). | ❌ | Uso interno. Puede publicarse selectivamente. |
| **PRY** | Proyecto | Contenido específico de un proyecto en desarrollo (Zona 2). | ✅ | Open source por defecto. |
| **COM** | Comunidad | Documentación orientada a colaboradores externos. | ✅ | Requiere campo `licencia`. |

> **Nota de migración v3.0 → v4.0:** El ámbito `GSM` (Guía Styl Master / NexusLab) se mantiene como categoría interna dentro de `OPE` y `GLB` si aplica, pero no como ámbito independiente. Los documentos `GSM` existentes migran a `OPE` o `GLB` según su alcance real. Ver historial al final de este documento.

---

## 2. Categorías (CAT)

Las categorías definen el **tipo funcional** de un documento dentro de su ámbito. Están organizadas por grupo temático.

### 2.1 Gobernanza y Sistema

| CAT | Nombre Completo | AMB Compatibles | Fecha Alta | Notas |
| :--- | :--- | :--- | :--- | :--- |
| **GOV** | Gobernanza | GLB | 2026-05-31 | Normas maestras del sistema documental. Solo maintainers. |
| **DIR** | Directrices | GLB, OPE | 2026-03-13 | Reglas de operación y proceso. *(heredado de v3.0)* |
| **MAT** | Matrices | GLB | 2026-05-31 | Catálogos controlados: códigos, siglas, vocabularios. |
| **MET** | Metadatos | GLB | 2026-03-14 | Esquemas YAML y parámetros IA. *(heredado de v3.0)* |
| **PLT** | Plantillas | GLB, OPE | 2026-03-13 | Formatos base para nuevas notas. *(ampliado a GLB)* |

### 2.2 Conocimiento y Proceso

| CAT | Nombre Completo | AMB Compatibles | Fecha Alta | Notas |
| :--- | :--- | :--- | :--- | :--- |
| **DEC** | Decisión de diseño | OPE, PRY | 2026-05-31 | Registro de decisiones con contexto y alternativas. |
| **ANA** | Análisis | GLB, OPE, PRY | 2026-03-14 | Auditorías, análisis de vacíos, estudios. *(ampliado a PRY)* |
| **LOG** | Bitácora | OPE, PRY | 2026-05-31 | Diario de desarrollo, entradas con fecha. |
| **HIS** | Historial | GLB | 2026-03-14 | Cronologías, hitos y trazabilidad del sistema. *(heredado)* |
| **REF** | Referencia | GLB, OPE, PRY | 2026-05-31 | Documentos de referencia, investigación aplicada. |
| **ACT** | Acta | OPE | 2026-05-31 | Registros de reuniones y decisiones grupales. |

### 2.3 Ingeniería y Producto

| CAT | Nombre Completo | AMB Compatibles | Fecha Alta | Notas |
| :--- | :--- | :--- | :--- | :--- |
| **PRO** | Producto | PRY | 2026-03-14 | Especificaciones de hardware/software. *(heredado)* |
| **INV** | Inventario | OPE, PRY | 2026-03-13 | BOM, listado de materiales/componentes. *(heredado)* |
| **SIM** | Simulación | PRY | 2026-05-31 | Documentos de análisis y simulación. |
| **MFG** | Manufactura | PRY | 2026-05-31 | Procesos y documentos de fabricación. |
| **CAL** | Cálculo | PRY | 2026-05-31 | Memorias de cálculo estructural y técnico. |

### 2.4 Comunidad y Comunicación

| CAT | Nombre Completo | AMB Compatibles | Fecha Alta | Notas |
| :--- | :--- | :--- | :--- | :--- |
| **TUT** | Tutorial | COM, GLB | 2026-05-31 | Guías paso a paso para colaboradores. |
| **CON** | Contribución | COM | 2026-05-31 | Pautas y flujos de contribución. |
| **VIS** | Identidad Visual | GLB | 2026-03-13 | Activos maestros: logos, paletas, tipografía. *(heredado)* |

---

## 3. Combinaciones válidas AMB × CAT

No todas las combinaciones de ámbito y categoría tienen sentido. Esta tabla es la referencia normativa.

| | GLB | OPE | PRY | COM |
|---|:---:|:---:|:---:|:---:|
| **GOV** | ✅ | — | — | — |
| **DIR** | ✅ | ✅ | — | — |
| **MAT** | ✅ | — | — | — |
| **MET** | ✅ | — | — | — |
| **PLT** | ✅ | ✅ | — | — |
| **DEC** | — | ✅ | ✅ | — |
| **ANA** | ✅ | ✅ | ✅ | — |
| **LOG** | — | ✅ | ✅ | — |
| **HIS** | ✅ | — | — | — |
| **REF** | ✅ | ✅ | ✅ | — |
| **ACT** | — | ✅ | — | — |
| **PRO** | — | — | ✅ | — |
| **INV** | — | ✅ | ✅ | — |
| **SIM** | — | — | ✅ | — |
| **MFG** | — | — | ✅ | — |
| **CAL** | — | — | ✅ | — |
| **TUT** | ✅ | — | — | ✅ |
| **CON** | — | — | — | ✅ |
| **VIS** | ✅ | — | — | — |

---

## 4. Proceso para agregar un código nuevo

1. Verificar que el código no exista ya (revisar secciones 1 y 2).
2. Abrir un issue en `woaion/governance` con el título `[MATRIZ] Propuesta: nuevo código [AMB|CAT] — [CÓDIGO]`.
3. Incluir: nombre completo, ámbitos compatibles, descripción funcional, al menos un ejemplo de uso.
4. Un maintainer revisa y, si se aprueba, actualiza este documento y cierra el issue.
5. Nunca usar un código en un documento antes de que aparezca en este registro.

---

## 5. Siglas de proyectos activos (referencia cruzada)

Estas siglas se usan en los códigos de artefactos de ingeniería (`SIGLA-SS-TIPO-NNN`). Se mantienen aquí como referencia; el registro normativo de proyectos está en `woaion/governance/01-matrices/`.

| Sigla | Proyecto | Estado |
| :--- | :--- | :--- |
| `J5C` | JS Cargo | Activo |
| `SCR` | Scrab – Salamander | Activo |
| `JSX` | JS Bot Futuro | Proyectado |
| `MK` | Taller Laboratorio MK | Activo |
| `ISE` | Índice de Simbiosis Ecológica | Activo |

---

## Historial de versiones

| Versión | Fecha | Cambios |
| :--- | :--- | :--- |
| 2.0.0 | 2026-05-31 | Migración a UDS v4.0. Nuevo UID, schema v4.0, categoría MAT. Ámbito GSM removido como AMB independiente. Nuevo AMB COM. Nuevas categorías: GOV, MAT, DEC, LOG, REF, ACT, SIM, MFG, CAL, TUT, CON. ANA y PLT ampliados. Tabla de combinaciones válidas agregada. |
| 1.0.0 | 2026-03-14 | Creación inicial (schema v3.0). Ámbitos: GLB, OPE, PRY, GSM. Categorías: DIR, PLT, VIS, INV, ANA, HIS, PRO, MET. |

---

[VER: 2026-05-31 | AGT: WOAION Core | ACC: Migración a UDS v4.0 — nuevo UID, AMB COM, 11 categorías nuevas, tabla de combinaciones, proceso de alta]
