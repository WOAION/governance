---
# ============================================================
# PLANTILLA ARF — Artefacto de Ingeniería (Capa 2)
# WOAION UDS v4.0
# Para: planos, cálculos, BOM, especificaciones técnicas
# ============================================================

uid: "[AAAAMMDD]_PRY_[CAT]_[NNN]_[nombre_descriptivo]"
titulo: "[SIGLA-SS-TIPO-NNN] — [Título descriptivo]"
ambito: PRY
categoria: "[PRO | INV | SIM | MFG | CAL | REF]"
estado: conceptual
fecha_creacion: "[YYYY-MM-DD]"
version: 0.1.0
version_estandar: "4.0"
autor: "[Nombre o handle]"
proyecto: "[SIGLA]"
proyecto_nombre: "[Nombre del proyecto]"

# --- Código de artefacto de ingeniería ---
codigo_artefacto: "[SIGLA-SS-TIPO-NNN]"
# Ejemplo: J5C-CHR-EST-001
# SIGLA: proyecto | SS: subsistema | TIPO: tipo | NNN: correlativo

# --- Versión del artefacto físico (plano/CAD) ---
# revision_plano: R01    # R01, R02, R03...
# version_completa: "0.1-R01"   # semántico + revisión

depende_de:
  # - "[UID de documento o código de artefacto del que depende]"
  # - "[Ej: J5C-CHR-EST-000 — Geometría base]"
  # - "[Ej: J5C-CHR-SIM-001 — Simulación que valida esta geometría]"

referenciado_por:
  # - "[Qué artefacto o documento usa a este]"

artefactos_relacionados: []

publico: true
tags:
  # - [subsistema]
  # - [tipo de análisis]
---

# [SIGLA-SS-TIPO-NNN] — [Título descriptivo]

| Campo | Valor |
|-------|-------|
| **Código** | [SIGLA-SS-TIPO-NNN] |
| **Proyecto** | [Nombre del proyecto] |
| **Subsistema** | [Nombre del subsistema] |
| **Tipo** | [Estructural / Mecánico / Eléctrico / Manufactura / Simulación / BOM / etc.] |
| **Estado** | conceptual |
| **Versión** | 0.1.0 |
| **Revisión plano** | R01 |
| **Autor** | [Nombre] |
| **Fecha** | [YYYY-MM-DD] |

---

## Descripción

*Qué es este artefacto. Una o dos oraciones que describan qué representa o qué hace.*

---

## Alcance y límites

*Qué incluye y qué no incluye. Con qué otros artefactos hace interfaz.*

**Incluye:**
- 

**No incluye (ver [código relacionado]):**
- 

---

## Especificaciones técnicas

*Los datos técnicos relevantes para este tipo de artefacto. Adaptar según el tipo:*

### Para planos / diseño estructural

| Parámetro | Valor | Unidad | Notas |
|-----------|-------|--------|-------|
| Material | | | |
| Dimensiones principales | | mm | |
| Masa estimada | | kg | |
| Carga de diseño | | N | |
| Factor de seguridad | | — | |

### Para BOM / lista de materiales

| Ref | Componente | Cantidad | Material | Proveedor | Notas |
|-----|-----------|----------|----------|-----------|-------|
| 001 | | | | | |

### Para cálculo

| Variable | Símbolo | Valor | Unidad | Fuente |
|----------|---------|-------|--------|--------|
| | | | | |

### Para simulación

| Parámetro | Valor |
|-----------|-------|
| Software | |
| Tipo de análisis | |
| Condiciones de contorno | |
| Mallado | |
| Resultado crítico | |

---

## Proceso de fabricación / uso

*Cómo se fabrica (si aplica) o cómo se usa este artefacto.*

---

## Validación

| Tipo | Estado | Referencia | Fecha |
|------|--------|-----------|-------|
| Cálculo analítico | ⬜ pendiente | | |
| Simulación | ⬜ pendiente | | |
| Prueba física | ⬜ pendiente | | |
| Revisión de par | ⬜ pendiente | | |

---

## Notas de diseño

*Decisiones de diseño embebidas en este artefacto, referencias a documentos DEC que lo justifican, y cosas a revisar en la siguiente versión.*

---

## Historial de revisiones

| Versión | Revisión | Fecha | Cambios |
|---------|----------|-------|---------|
| 0.1.0 | R01 | [YYYY-MM-DD] | Creación inicial |
