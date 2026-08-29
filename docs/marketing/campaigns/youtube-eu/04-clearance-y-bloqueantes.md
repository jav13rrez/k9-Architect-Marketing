# YouTube España + Europa — Clearance de claims y bloqueantes UE

**Contrastado contra:** `docs/product/RELEASE-READINESS-AND-CLAIMS.md` · `docs/product/PRODUCT-REFERENCE.md` · `docs/marketing/research/investigacion-mercado-fase-2-2026-08-22.md` · `docs/marketing/research/naming-logo-audit-2026-08-22.md`
**Hermanos:** [01 · Visión](01-vision-y-estrategia.md) · [02 · Territorios](02-territorios-creativos.md) · [03 · Arquitectura](03-arquitectura-youtube.md)

Regla de decisión heredada, literal:

```text
implementada + desplegada + verificada en su plataforma/rol + respaldada por copy exacto
```

---

## 1. Rótulos y líneas de la serie A

La serie A vende **restricción**. Eso la hace muy segura en promesa comercial y muy exigente en fidelidad de interfaz: si enseñamos una pantalla que el producto no muestra, el argumento entero se cae ante el único público capaz de comprobarlo.

| # | Cadena / línea | Pieza | Capacidad | Estado | Nota |
|---|---|---|---|---|---|
| 1 | `Plan rechazado — revisión de bienestar` | A1, A4 | Welfare Reviewer con veto | **APTO en capacidad · REVISAR en literal** | El veto es *VERIFICADO con gate condicionado*. **Debe reproducirse el texto real de la pantalla de veto.** Si esa pantalla no existe hoy con ese literal, se construye antes de rodar. No se inventa una interfaz para un anuncio. |
| 2 | `Motivo: exposición por encima del umbral seguro para la edad` | A1 | Topes por edad y reglas direccionales | **REVISAR** | Debe corresponder a un motivo que el revisor emite realmente. Si el producto no devuelve motivo legible, o se añade o se elimina el rótulo. |
| 3 | «Este plan lo ha generado nuestra IA. Y nuestro propio sistema lo ha rechazado.» | A1 | — | **APTO** | Describe el mecanismo. No afirma que el veto sea infalible. |
| 4 | «Un generador que nunca dice que no, no es una herramienta. Es un riesgo con buena interfaz.» | A1 | — | **APTO** | Afirmación de categoría, no comparación con competidor nombrado. No atribuye defectos concretos a productos identificables. |
| 5 | `Revisión de bienestar · Ajuste profesional · Auditoría` | A1 | Tres capacidades verificadas | **APTO** | — |
| 6 | `Plan en pausa` + `Incidente reportado en sesión · derivación recomendada` | A2, A4 | Guard de sesión / `SAFETY_HOLD` | **APTO en capacidad · REVISAR en literal** | *VERIFICADO en código y pruebas*; el registro pide verificar la UX de cada categoría en producción antes de una demostración pública crítica. Un anuncio lo es. |
| 7 | `ATENCIÓN · incidente reportado` | A2 | Panel de atención | **APTO** | Señales verificadas: estrés reciente, estancamiento, resultado bajo. |
| 8 | «La decisión de qué hacer sigue siendo tuya.» | A2 | Criterio profesional | **APTO** | Redacción segura recomendada por el registro. |
| 9 | `Esta consulta no se responde aquí.` + `Recomendación: valoración veterinaria` | A3 | Bandera roja de Consulta IA | **BLOQUEADO** | Consulta IA: *IMPLEMENTADO / VERIFICAR PRODUCCIÓN* en ambos roles. No se produce hasta cerrar smoke test con caso real. |
| 10 | `Fuentes · No modifica el plan` | A3 | Fuentes disponibles; no altera el plan | **APTO cuando se desbloquee A3** | Decir «muestra fuentes disponibles», nunca «todas las respuestas están demostradas». |
| 11 | `Consulta IA es un sistema de IA.` | A3 | — | **OBLIGATORIO** | Ver §2. |
| 12 | `Júzgalo por lo que se niega a hacer.` | A1, A2, A4 | — | **APTO** | Sin promesa de resultado. |
| 13 | `Del caso al informe.` | A1, A2 | Firma B2B vigente | **APTO** | Ya en uso en la campaña B2B. |
| 14 | `Aplicación web` | Todas | Plataforma | **APTO · OBLIGATORIO** | Prohibido «disponible en iOS/Android» y todo badge de tienda. |

## 2. Rótulos y líneas de la serie B y C

| # | Cadena / línea | Pieza | Estado | Nota |
|---|---|---|---|---|
| 15 | `Sin cortes` + «no hemos quitado nada» | B1, B2 | **APTO con condición** | Solo si es literalmente cierto. Si se corta un fragmento, hay que decirlo en pantalla. Esta pieza vive de que la afirmación sea comprobable. |
| 16 | `2/5 · señales: jadeo` | B1, B2 | **APTO** | Campos reales del reporte de sesión. |
| 17 | `REDUCIR UNA DIMENSIÓN · 8 m → 12 m` | B1, B2 | **APTO** | 2/5 = 40 %, por debajo del 50 %, con dificultad excesiva identificable → reducir una dimensión. Coincide con la regla implementada. |
| 18 | «Una dificultad cada vez.» | B2 | **APTO** | Principio 2 del producto. |
| 19 | `Práctica reportada` | B1, B2 | **APTO · OBLIGATORIO** | **Nunca «deberes».** No existe subsistema de deberes con asignación, plazo ni recordatorio. |
| 20 | «El informe lleva el nombre del negocio en texto, no un logotipo» | B1 | **APTO** | Es exactamente la redacción segura del registro. Decirlo en voz alta es parte del argumento. |
| 21 | Bloque 7: lista de lo que K9 **no** hace | B1 | **APTO · RECOMENDADO** | Debe recitar el apartado «Funcionalidades que no se pueden prometer todavía». Es el activo de credibilidad. |
| 22 | `A VECES DEBE DECIR: PARA` · `PAUSA Y DERIVACIÓN` · `NO ES UNA GARANTÍA` | C1 | **APTO** | Heredado sin cambios de la pieza B2C C05 ya aprobada. |
| 23 | `Un paso cada vez.` | C1, C2 | **APTO** | Firma B2C vigente. |
| 24 | Cualquier mención de precio o prueba | Todas | **FUERA** | Ninguna pieza menciona precio ni prueba. Deliberado: solo hay evidencia de **un** flujo Pro de Stripe. Si se añadiera, quedaría condicionado a verificar los seis precios. |

---

## 3. Bloqueantes de la Unión Europea

### B1 · Transparencia de IA — artículo 50 del AI Act

**Desde el 2 de agosto de 2026 son aplicables** obligaciones de transparencia del artículo 50 del Reglamento (UE) 2024/1689 para determinadas interacciones con IA. La propia investigación del repositorio lo recoge y concluye que **K9 debe informar claramente de que Consulta IA es un sistema de IA** y revisar con asesoría competente su papel, documentación y comunicaciones.

Impacto concreto sobre esta campaña:

- La pieza **A3 no se emite** sin el aviso y sin revisión legal.
- Toda pieza que muestre a la IA generando o respondiendo debe poder identificar el sistema como IA de forma clara. La serie A lo hace de forma natural —dice «nuestra IA» en voz alta— pero el cumplimiento no se deduce del tono: se documenta.
- Si alguna creatividad usara **material generado sintéticamente** (voz, rostro, plano), aplica además el régimen de etiquetado que corresponda, y las propias reglas de divulgación de contenido alterado o sintético de YouTube. Recomendación: no usar generativo en esta campaña. No aporta nada a un formato que vive de la grabación de pantalla real.

`Consulta IA es un sistema de IA.` es el literal mínimo en pantalla. La redacción final la fija la revisión legal, no marketing.

### B2 · Consentimiento y medición en el EEE

El registro de pendientes deja abiertos **políticas legales enlazadas y banner/gestión de cookies**. Consecuencia:

> **No se puede activar remarketing, públicos ni seguimiento de conversiones de plataforma para tráfico del EEE hasta tener consentimiento operativo.** Google exige cumplimiento de su política de consentimiento de usuarios de la UE y señalamiento de consentimiento para medición y públicos en el EEE.

- La Fase 1 se diseña para funcionar **sin** eso: UTM, analítica de servidor y registro manual. Ver [03 · §3](03-arquitectura-youtube.md).
- **No es un bloqueante de la campaña; es un bloqueante del remarketing.** La distinción importa: se puede empezar, no se puede optimizar como se optimizaría normalmente.
- Antes de instalar cualquier píxel: banner operativo, política publicada y revisión jurídica. Instalar medición primero y legalizar después es exactamente el orden que el registro prohíbe.

### B3 · Marca en España y UE

La auditoría de naming recomienda `K9 Architect` **condicionado a búsqueda profesional de anterioridades**, y señala expresamente que debe consultarse marcas nacionales, nombres comerciales, internacionales con efecto en España y **marcas de la UE**, con la advertencia de la EUIPO de que una búsqueda reduce el riesgo pero no lo elimina. La consulta RDAP de `k9architect.com` devolvió ausencia de registro, lo que **no garantiza** disponibilidad.

Una campaña paneuropea multiplica la exposición respecto a una campaña española. **Cierra antes de la primera impresión pagada.**

### B4 · Divulgación de la relación comercial en el Territorio D

El programa de profesionales piloto genera contenido pagado o incentivado publicado por terceros. Requiere:

- Divulgación clara y visible de la relación comercial, conforme a la normativa española y europea de publicidad y competencia desleal, y a las reglas de contenido de marca de YouTube.
- Contrato que fije divulgación, uso de imagen, consentimiento de casos y **el derecho del profesional a discrepar en cámara**.
- Ninguna aprobación editorial previa de K9 sobre el juicio del profesional. Esa es la condición que hace válido el activo, y también la que evita que la divulgación se convierta en publicidad encubierta.

### B5 · Casos, imagen y datos

- Caso **compuesto o anonimizado con autorización verificable**. La estrategia vigente prohíbe publicar casos reales identificables o imágenes de clientes sin consentimiento específico.
- Rótulo `DATOS DE DEMOSTRACIÓN` permanente en toda interfaz mostrada.
- Ningún dato personal real en pantalla, incluida la barra de navegación, notificaciones del sistema y nombres de archivo durante la grabación de B1.

---

## 4. Riesgos específicos de este emplazamiento

| Riesgo | Lectura | Mitigación |
|---|---|---|
| **Adyacencia aversiva** | El anuncio se reproduce antes de contenido de castigo o collar eléctrico. Destruye el posicionamiento ante el público objetivo y es capturable. | Lista blanca manual, exclusiones a nivel de cuenta, revisión trimestral, salida en 24 h. [01 · §6](01-vision-y-estrategia.md). |
| **Anunciar a quien quieres como cliente** | La serie A se emite en canales de profesionales… vendiendo software a profesionales. Algunos lo verán como intrusión. | El mensaje es de restricción, no de sustitución. Ninguna pieza dice ni sugiere que K9 reemplace al profesional. Es la razón por la que el territorio del veto es también el más seguro socialmente. |
| **Un profesional del piloto critica en público** | Ocurrirá. | Es el diseño, no el accidente. Una crítica pública respondida con corrección vale más que diez testimonios comprados. La estrategia vigente ya obliga a corregir públicamente un error metodológico detectado. |
| **Comentarios pidiendo consejo sobre un perro concreto** | El activo largo los generará. | Protocolo ya definido en la estrategia: no diagnosticar en comentarios, no prescribir protocolo individual, derivar. Asignar responsable antes de publicar B1, no después. |
| **Saturación de la lista blanca** | Inventario pequeño, público que se conoce entre sí. | Límite de frecuencia desde el arranque y rotación programada. [03 · §2.3](03-arquitectura-youtube.md). |

---

## 5. Checklist de aprobación por pieza

Antes de subir cualquier creatividad a la cuenta:

- [ ] Cada pantalla mostrada **existe en el producto desplegado**, con ese literal.
- [ ] Rótulo `DATOS DE DEMOSTRACIÓN` presente y legible.
- [ ] Ninguna capacidad depende de un flag sin experiencia asociada.
- [ ] Ninguna cifra de negocio, tasa de éxito, testimonio, logo ni plazo.
- [ ] «Prácticas reportadas», no «deberes». «Hipótesis de trabajo», no «diagnóstico». «Aplicación web», no app de tienda.
- [ ] «Por encima del 80 %», nunca «80 % o más».
- [ ] Ninguna salvaguarda presentada como garantía absoluta.
- [ ] Subtítulos quemados y revisados; la pieza se entiende sin sonido.
- [ ] Aviso de IA presente donde aplique.
- [ ] Landing de destino dice lo mismo que la pieza.
- [ ] **B3 cerrado** — marca y dominio asegurados en España y UE.
