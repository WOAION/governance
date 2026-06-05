# WOAION — Sistema de Licencias
### Open Industrial Platform License Stack (OIPLS v1.0)

Este proyecto adopta un sistema de licencias por capas para equilibrar libertad de uso, comercialización, colaboración abierta y protección de identidad de marca.

---

## Resumen

| Componente | Licencia |
|---|---|
| Hardware · Diseño físico · CAD · PCB | CERN-OHL-S v2 |
| Firmware · Código embebido | GPLv3 |
| Software · Apps · Herramientas | AGPLv3 |
| Documentación · Manuales · Wiki | CC BY-SA 4.0 |
| Marca · Nombre · Logotipo | Todos los derechos reservados |

---

## Filosofía

**Se permite:**
- Fabricar unidades físicas
- Modificar el diseño
- Vender productos derivados
- Usar comercialmente el sistema
- Mejorar el proyecto
- Crear variantes industriales, agrícolas o civiles

**Siempre que:**
- Se mantenga atribución al proyecto original (WOAION)
- Las mejoras derivadas se compartan bajo la misma licencia correspondiente
- No se use la marca oficial sin autorización expresa

---

## Aplicación por repositorio

| Repositorio | Componente | Licencia |
|---|---|---|
| `governance` | Documentación / normas | CC BY-SA 4.0 |
| `j5-cargo` | Hardware / planos / CAD | CERN-OHL-S v2 |
| `j5-cargo/docs` | Documentación técnica | CC BY-SA 4.0 |
| `ise` | Documentación / metodología | CC BY-SA 4.0 |
| `docs` | Tutoriales / guías públicas | CC BY-SA 4.0 |

---

## Estructura de licencias en repositorios de hardware

Cada repositorio de hardware (j5-cargo, scrab, jsx-bot) mantiene esta estructura:

```
[proyecto]/
├── hardware/         → LICENSE (CERN-OHL-S v2)
├── firmware/         → LICENSE (GPLv3)
├── software/         → LICENSE (AGPLv3)
├── docs/             → LICENSE (CC BY-SA 4.0)
├── branding/         → TRADEMARK.md
└── LICENSE_STACK.md  → este documento (copia)
```

---

## Marca registrada

El nombre **WOAION**, el logotipo y los identificadores visuales asociados son propiedad de WOAION y están protegidos. No pueden usarse en productos derivados sin autorización expresa.

Para consultas sobre uso de marca: woaionoficial@gmail.com

---

*WOAION · OIPLS v1.0 · 2026*
