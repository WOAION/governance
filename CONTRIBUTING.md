# Contribuir a WOAION

Gracias por tu interés en contribuir al ecosistema WOAION. Este archivo explica cómo participar de manera ordenada y coherente con el resto del proyecto.

---

## Antes de contribuir

WOAION usa un **Sistema de Documentación Unificado (UDS)** que define cómo se nombran, clasifican y organizan todos los documentos. Leer el documento `00_WOAION_UDS_sistema_unificado.md` en el repositorio `woaion/governance` te va a ahorrar tiempo y asegurar que tu contribución sea compatible.

**No es necesario entender todo el sistema para contribuir.** Con leer esta guía y usar las plantillas correctas alcanza para empezar.

---

## Tipos de contribución

### 🐛 Reportar un problema

Si encontraste un error en la documentación, un plano incorrecto, o algo que no funciona como se describe:

1. Abrí un **Issue** en el repositorio correspondiente
2. Usá el título: `[TIPO] Descripción breve del problema`
   - `[ERROR]` para errores técnicos o de contenido
   - `[MEJORA]` para sugerencias de mejora
   - `[PREGUNTA]` para dudas que podrían indicar documentación faltante

---

### 📝 Mejorar documentación existente

Para correcciones menores (typos, links rotos, clarificaciones):

1. Hacé un fork del repositorio
2. Editá el archivo directamente
3. Abrí un Pull Request con el título: `fix: descripción breve`
4. No cambies el `uid` ni bajes el `estado` del documento

---

### ✨ Agregar contenido nuevo

Para tutoriales, guías, análisis, o cualquier documento nuevo:

1. Verificá que no exista algo similar (buscá en `01_REGISTRO_CATEGORIAS.md`)
2. Elegí la plantilla correcta del repositorio `woaion/governance/02-plantillas/`
3. Generá el UID correcto: `AAAAMMDD_AMB_CAT_NNN_nombre`
4. Si necesitás una categoría nueva, registrala **primero** en el issue `[MATRIZ] Nueva categoría: XXX`
5. Empezá con `estado: draft`
6. Abrí un Pull Request con el título: `feat: descripción breve`

---

### 🔧 Contribuir artefactos de ingeniería (planos, CAD, BOM)

Los artefactos de ingeniería usan el sistema de códigos `[SIGLA]-[SS]-[TIPO]-[NNN]`:

1. Verificá el último número correlativo en el proyecto correspondiente
2. Usá la plantilla `PLT_artefacto_ingenieria.md` para la documentación asociada
3. Empezá con `estado: conceptual`
4. Incluí siempre un documento de decisión (`PLT_decision_diseno.md`) si cambiás algo significativo

---

## Formato y estilo

- Todos los documentos en Markdown (`.md`)
- Frontmatter YAML obligatorio (ver plantillas)
- Idioma principal: español. Traducciones al inglés son bienvenidas (agregar `.en.md` al nombre)
- `snake_case` para nombres de archivo, sin acentos, sin espacios
- Fechas en ISO 8601: `2026-05-31`
- No uses tabs en YAML, solo espacios

---

## Qué NO aceptamos

- Documentos sin frontmatter YAML
- Modificaciones directas a normas `GLB` o `GOV` (abrí un issue primero)
- Cambiar el estado de un documento a `certified` (solo maintainers)
- Crear nuevos códigos AMB sin pasar por el proceso de RFC
- Contenido que no tenga relación con los proyectos activos de WOAION

---

## Proceso de revisión

Una vez que abrís un Pull Request:

1. Un maintainer lo revisa dentro de 7 días
2. Si hay cambios pedidos, tenés 14 días para responder
3. Una vez aprobado, el maintainer hace el merge y actualiza el estado del documento
4. Tu nombre o handle se agrega al campo `contribuidores` del frontmatter

---

## Código de conducta

WOAION es un proyecto colaborativo y abierto. Esperamos que todas las interacciones sean respetuosas, constructivas y orientadas al aprendizaje compartido. No se tolera ningún tipo de discriminación o acoso.

Para reportar una situación, escribí a [correo de contacto].

---

## ¿Preguntas?

Abrí un Issue con el prefijo `[PREGUNTA]` o unite al canal de la comunidad en [link].

---

*CONTRIBUTING.md · WOAION UDS v4.0 · CC-BY-SA 4.0*
