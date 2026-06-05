---
# ============================================================
# PLANTILLA DEC — Registro de Decisión de Diseño
# WOAION UDS v4.0
# ============================================================

uid: "[AAAAMMDD]_[PRY|OPE]_DEC_[NNN]_[nombre_descriptivo]"
titulo: "DEC-[NNN] — [Título de la decisión]"
ambito: PRY
categoria: DEC
estado: draft
fecha_creacion: "[YYYY-MM-DD]"
version: 1.0.0
version_estandar: "4.0"
autor: "[Nombre o handle]"
proyecto: "[SIGLA]"
proyecto_nombre: "[Nombre del proyecto]"

depende_de:
  # - "[UID de análisis o cálculo que motivó esta decisión]"
  # - "[SIGLA-SS-TIPO-NNN de artefacto relacionado]"

artefactos_relacionados:
  # - "[SIGLA-SS-TIPO-NNN que implementa esta decisión]"

publico: true
tags:
  - decision
  # - [subsistema]
  # - [material | geometria | proceso | ...]
---

# DEC-[NNN] — [Título de la decisión]

| Campo | Valor |
|-------|-------|
| **Proyecto** | [Nombre del proyecto] |
| **Subsistema** | [Subsistema afectado] |
| **Fecha** | [YYYY-MM-DD] |
| **Estado** | draft |
| **Decide** | [Nombre/handle] |

---

## La decisión

*En una o dos oraciones: qué se decidió hacer.*

> **Decidimos usar [X] para [propósito] en lugar de [Y].**

---

## Contexto

*Por qué era necesario tomar esta decisión. Qué restricciones existían (costo, tiempo, herramientas disponibles, conocimiento del equipo, fase del proyecto). Sin contexto, la decisión parece arbitraria.*

---

## Opciones evaluadas

### Opción A — [Nombre de la opción elegida] ✅

**Descripción:** 

**Ventajas:**
- 

**Desventajas:**
- 

**Por qué se eligió:** 

---

### Opción B — [Nombre de alternativa] ❌

**Descripción:** 

**Por qué se descartó:** 

---

### Opción C — [Nombre de alternativa] ❌ *(si aplica)*

**Descripción:** 

**Por qué se descartó:** 

---

## Consecuencias

*Qué implica esta decisión: impacto en peso, costo, tiempo, complejidad, mantenibilidad, reversibilidad. Ser honesto sobre los trade-offs.*

**Positivo:**
- 

**Negativo / a monitorear:**
- 

**Condición para revisitar esta decisión:**
*En qué circunstancias debería reconsiderarse esta decisión (ej: si el peso total supera X kg, si aparece un proveedor Y).*

---

## Referencias

- `[UID o código]` — Descripción

---

## Historial

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0.0 | [YYYY-MM-DD] | Decisión inicial registrada |
