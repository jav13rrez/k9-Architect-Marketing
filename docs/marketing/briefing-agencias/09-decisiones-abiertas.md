# 09 · Decisiones abiertas del cliente

**Informativa. Se comparte en abierto porque afecta al trabajo.**
Hermanos: [04 · Dirección de arte](04-direccion-de-arte.md) · [06 · Claims](06-claims-y-guardrails.md)

**Última actualización:** agosto de 2026. Tres puntos se han cerrado desde la primera versión del paquete; quedan marcados como resueltos para que nadie trabaje sobre información caducada.

Ninguna decisión abierta bloquea el pensamiento estratégico ni la conceptualización. Algunas bloquean arte final, producción o emisión.

---

## ✅ D1 · Identidad visual · RESUELTO en dirección · abierto solo en elección

**La huella roja ha sido retirada.** El activo `assets/logo.svg` ya no existe. La identidad es un **wordmark sin glifo**, coherente con la dirección aprobada en la auditoría de naming y logo.

`design-system/assets/K9 Architect logo options/`

**Cerrado:**
- Sin glifo, sin huella, sin símbolo. Wordmark tipográfico.
- `K` en neutro, **`9` en rojo K9 `#ef4444`**, «Architect» a continuación.
- Marca cuadrada para icono, favicon y avatar: **solo tipografía**.

**Abierto:** elegir entre **1A · inline** (contraste por peso) y **1B · apilado** (`ARCHITECT` en mono con interletrado abierto).

**Efecto:** 🟡 se puede conceptar y maquetar con cualquiera de las dos. **No se cierra arte final** hasta la elección. Detalle en [04 · §4](04-direccion-de-arte.md).

**Pendiente técnico:** la tipografía del wordmark elegido debe entregarse **trazada a contornos**. Ningún archivo de marca puede depender de una fuente por ruta externa.

---

## ✅ D2 · Paleta de neutros · RESUELTO

> **`design-system/colors_and_type.css` es la fuente de verdad.** Decisión cerrada.

| Rol | Token | Hex |
|---|---|---|
| Fondo de página | `--bg-page` | `#1a1b1e` |
| Superficie / card | `--bg-card` | `#25262b` |
| Sidebar | `--bg-sidebar` | `#1e1f24` |
| Borde sutil | `--border-subtle` | `#373a40` |

La escala `#0f1013 / #1a1b1e / #2c2e33` que aparecía en briefs de campaña anteriores **queda superada**. Ya no hay dos sistemas: la atmósfera de campaña y las pantallas de producto usan la misma paleta.

**Un punto de negro más profundo sigue siendo válido como decisión de grado cinematográfico**, pero no es un color de marca y no se usa para maquetar superficies.

**Azul `#3b82f6`, teal `#14b8a6` y morado `#8b5cf6`** aparecen documentados como superposiciones en `design-system/CLAUDE.md` pero **no existen como primitivas** en el CSS. Fuera de la publicidad. Queda como punto abierto interno del sistema de diseño, no del briefing.

---

## 🔴 D3 · Clearance de marca · BLOQUEA EMISIÓN

`K9 Architect` está recomendado como marca pública **condicionado a búsqueda profesional de anterioridades** en OEPM y EUIPO, incluidas variaciones fonéticas y gráficas. La consulta del dominio devolvió ausencia de registro, lo que **no garantiza** disponibilidad.

**Por qué es el bloqueante más serio:** es el único de esta lista sin arreglo posterior. Una campaña emitida con el nombre sin asegurar es irreversible.

**Qué falta:** búsqueda profesional cerrada, dominio y activos sociales reservados, decisión de transición desde «K9 Behavioral Architect».

---

## ✅ D4 · Voz del sistema de diseño · RESUELTO · queda el casing

`design-system/README.md` **ha sido reescrito** para reflejar el registro de claims. Correcciones aplicadas:

- Eliminada toda referencia a **«clinical»**, «clinic», «patient», «treatment» y «therapy».
- Eliminada la descripción **«AI-powered SaaS platform»**: la IA es mecanismo, no promesa.
- Corregido **«scientific corpus»** y **«evidence-based protocols»** → corpus especializado, con fuentes disponibles.
- Corregida la audiencia: ya no es «elite canine behaviorists», sino **dos roles vinculados**, dueño y profesional.
- Eliminada la capacidad **«health tracking»**: no existe en el producto.
- Eliminado el vocabulario **«kennel»**: no existe en el producto.
- Retirado el icono **`paw-print`**, más `brain` y `bot`.
- Añadida una sección **Claims-safe language** vinculante, con tabla de vocabulario prohibido, reglas de copy sobre IA y sobre resultados, y semántica de color.
- Añadida una tabla de **inconsistencias conocidas** para que se corrijan en vez de propagarse.

**Abierto:** el **casing de la interfaz de producto** (Title Case en navegación) frente al de comunicación (sentence case siempre). Son convenciones distintas y deliberadas. Unificarlas es decisión de Dirección Artística.

**Efecto:** 🟡 ninguno sobre producción publicitaria. En comunicación manda [01](01-plataforma-de-marca.md): **sentence case, siempre**.

---

## 🟠 D5 · Verificación de Consulta IA · bloquea piezas concretas

Implementada en código para ambos roles, **pendiente de verificación en producción**. Además activa obligaciones de transparencia del artículo 50 del AI Act desde el 2 de agosto de 2026.

**Efecto:** no puede ser eje principal de campaña. Cualquier pieza que la muestre queda condicionada.

---

## 🟠 D6 · Catálogo de precios y facturación · bloquea toda mención de precio

Solo hay evidencia de compra verificada para **un** flujo Pro. Los seis precios, los intervalos mensual y anual, el portal de facturación y los eventos posteriores de Stripe no están todos probados.

**Efecto:** ninguna pieza menciona precio ni prueba sin autorización escrita. Ver [06 · §5](06-claims-y-guardrails.md).

---

## 🔴 D7 · Legal y consentimiento · BLOQUEA CAMPAÑA DE PAGO

Pendientes: políticas de privacidad y términos reales enlazados, revisión jurídica del tratamiento de datos y de los claims, **banner y gestión de cookies**, y flujo visible de eliminación de cuenta.

**Efecto directo sobre medios:** sin consentimiento operativo **no hay remarketing ni seguimiento de conversiones legítimo para tráfico del EEE**. La campaña puede arrancar midiendo con UTM, analítica de servidor y registro manual, pero no puede optimizarse como sería habitual.

---

## 🟡 D8 · Prueba social · condiciona el enfoque

**No existe ninguna.** Ni testimonios, ni valoraciones, ni logos, ni premios, ni cifras de usuarios.

**Efecto creativo:** toda la credibilidad se construye con **mecanismo y honestidad**, no con validación de terceros. No es un obstáculo temporal que el presupuesto vaya a tapar: es la condición de partida, y el trabajo que la asuma de frente será mejor que el que intente disimularla.

---

## Resumen para producción

| # | Decisión | Estado | Bloquea |
|---|---|---|---|
| D1 | Identidad visual | ✅ Dirección cerrada · elección abierta | 🟡 Arte final |
| D2 | Paleta de neutros | ✅ **Resuelto** — el CSS manda | — |
| D3 | Clearance de marca | 🔴 Abierto | **Emisión** |
| D4 | Voz del design system | ✅ **Resuelto** — queda el casing | 🟡 Nada |
| D5 | Verificación de Consulta IA | 🟠 Abierto | Piezas que la muestren |
| D6 | Catálogo de precios | 🟠 Abierto | Toda mención de precio |
| D7 | Legal y consentimiento | 🔴 Abierto | **Campaña de pago** |
| D8 | Prueba social | 🟡 Condicionante | Nada |

**Se puede conceptar y maquetar hoy. No se puede emitir hasta cerrar D3 y D7.**
