# K9 Architect — NFL Spot V3 · Brief estratégico

**Pieza:** Spot de 60 s para pausa comercial de la final de la NFL + cutdowns
**Rol:** Dirección Creativa Ejecutiva / Realización
**Fecha:** agosto de 2026
**Fuentes:** `docs/product/*`, `docs/marketing/research/*`, `docs/marketing/campaigns/b2b|b2c/*`, `design-system/colors_and_type.css`
**Documentos hermanos:** [02 · Guion 60 s](02-guion-spot-60s.md) · [03 · Prompts de producción](03-prompts-produccion-video.md) · [04 · Clearance de claims](04-clearance-de-claims.md)

---

## 0. Confirmación de dirección

Entendido. Antes de una sola línea de guion, así queda fijado el encargo:

| Eje | Lectura asumida |
|---|---|
| **Estrategia de atención** | No competimos por volumen. En una pausa donde todo grita, el recurso escaso es el silencio. Entramos como una caída de nivel, no como un pico. |
| **Voz** | Profesional de igual a igual. Directo, preciso, sereno, observacional. Sin gurú, sin coach, sin épica. |
| **Certeza** | Absoluta sobre el proceso. Cero sobre el resultado del animal. Ni una promesa de conducta. |
| **Tecnología** | Mecanismo que informa. Nunca magia que decide. La IA no firma la decisión en pantalla; la firma una persona. |
| **Emoción** | Reconocida, no explotada. Se muestra la tensión real de un dueño; no se fabrica melodrama ni culpa. |
| **Sistema visual** | Oscuro, estructurado, preciso. Pantallas reales. Sin holografía, sin destellos de IA, sin estética corporativa tech. |
| **Bienestar animal** | Ningún animal expuesto a reactividad provocada para conseguir un plano. Esto condiciona el guion entero, no solo el rodaje. |

---

## 1. Qué cambia respecto a V2

V2 (`nfl-spot-v2/`) resolvió bien el tono y dejó un territorio sólido —«El Umbral»— pero tiene tres carencias que V3 corrige:

| # | Carencia de V2 | Corrección en V3 |
|---|---|---|
| 1 | El encargo pedía **prompts de producción con cinco bloques obligatorios cada uno**. V2 entregó tres prompts sueltos en prosa, sin la estructura. | [03](03-prompts-produccion-video.md) entrega **10 prompts, cada uno con los cinco bloques completos** más su cadena lista para pegar en el motor. |
| 2 | El territorio («la distancia correcta») es correcto pero **descriptivo**: cuenta lo que hace el producto. No produce el «entiendo el problema por primera vez». | V3 se construye sobre una **inversión**: el momento heroico del spot es un retroceso deliberado. |
| 3 | Ninguna línea estaba contrastada contra `RELEASE-READINESS-AND-CLAIMS.md`. Varios rótulos eran publicables; otros no lo son sin verificación. | [04](04-clearance-de-claims.md) audita **cada rótulo y cada línea de voz** contra el registro de promesas, con estado y condición de salida. |

V2 no se descarta: su cutdown de 15 s y su nota de dirección siguen siendo válidos. V3 los sustituye por versiones alineadas al nuevo territorio.

---

## 2. El insight

En la investigación de Fase 1 hay una frase literal de un dueño que vale más que cualquier claim que podamos escribir:

> «Every step forward is two steps back.»
> — r/reactivedogs, recogido en `investigacion-mercado-fase-1-2026-08-22.md`

Y su equivalente profesional:

> «People challenging me, asking why their dogs aren't "better" yet.»
> — r/dogtrainers, misma fuente

Las dos frases describen el mismo agujero: **nadie ha explicado nunca que retroceder es una decisión técnica, no un fracaso.** El dueño lo vive como derrota. El profesional lo tiene que defender sin datos delante.

Y es exactamente lo que el motor de K9 hace de forma determinista. La regla implementada, literal:

```text
Menos del 50 % con una dificultad excesiva identificable  →  reducir una dimensión
Éxito entre 50 % y 80 %                                   →  repetir para consolidar
Estrés con éxito alto                                     →  no avanzar
```

El producto ya trata el paso atrás como una salida legítima del sistema. Nadie lo ha contado nunca.

---

## 3. Territorio creativo: «Dos pasos atrás»

> **Concepto central:** el spot cuya escena climática es una persona retrocediendo a propósito.

Por qué funciona en esta pausa concreta y en ninguna otra:

- **Contraste de categoría.** La NFL es el deporte de las yardas ganadas. Retroceder es, literalmente, la unidad de fracaso del acontecimiento que estamos interrumpiendo. Un anuncio cuyo héroe cede terreno a propósito produce una disonancia que obliga a mirar. No hace falta enseñar un balón ni mencionar el fútbol: la resonancia la pone el contexto de emisión.
- **Reconocimiento inmediato.** Cualquiera que haya paseado un perro reactivo ha dado esos dos pasos. Los ha dado avergonzado. El spot le dice que eran correctos.
- **Demuestra el mecanismo sin explicarlo.** El retroceso *es* la regla del motor ejecutándose. No hay que narrar la IA: se ve una decisión.
- **Es imposible de firmar por un competidor.** Dogo, Woofz o Canivox no pueden decir esto: sus productos no tienen una lógica de reducción de dimensión que puedan enseñar en pantalla.
- **No promete nada.** Es el único territorio que da una satisfacción emocional completa sin afirmar ni una vez que el perro mejora.

### Línea del spot

```text
A veces el siguiente paso va hacia atrás.
Lo que cambia es que ahora sabes por qué.
```

### Firma de marca (ya en uso, no se toca)

```text
Un paso cada vez.
```

Procede del end card B2C vigente en `campaigns/b2c/`. V3 la mantiene por consistencia con la campaña de pago ya guionizada.

---

## 4. Qué escucha cada público en el mismo minuto

| Público | Su dolor documentado | Qué oye en este spot |
|---|---|---|
| **Dueño (B2C)** | Parálisis por sobreinformación; los retrocesos parecen fracaso [F1-DUE-05, F1-DUE-06]. | «Ese paso atrás que llevo dando dos años tiene nombre y es una decisión.» |
| **Profesional (B2B)** | Ceguera entre citas; «sí, bien» no es seguimiento [F1-PRO-01, F1-PRO-05]. | «Lo que ella reporta llega a mi caso con intentos, señales y contexto. Puedo defender el proceso.» |
| **Sector / inversión** | Categoría llena de apps de trucos y CRM administrativos. | «Esto no es contenido. Es una capa de decisión con reglas, límites y trazabilidad.» |

El guion no reparte 30 s a cada uno. Reparte **un solo caso visto desde los dos lados**, que es exactamente la arquitectura del producto: `caso → criterios → práctica reportada → atención → informe`.

---

## 5. Sistema visual

### 5.1 Paleta — fuente de verdad

**`design-system/colors_and_type.css` es la fuente de verdad.** Decisión cerrada por el cliente.

| Rol | Token | Hex |
|---|---|---|
| Fondo de página | `--bg-page` | `#1a1b1e` |
| Superficie / card | `--bg-card` | `#25262b` |
| Sidebar | `--bg-sidebar` | `#1e1f24` |
| Borde sutil | `--border-subtle` | `#373a40` |
| Rojo K9 | `--red-500` | `#ef4444` |
| Verde criterio | `--green-500` | `#10b981` |
| Ámbar atención | `--orange-500` | `#f59e0b` |

La escala `#0f1013 / #1a1b1e / #2c2e33` que se usó en briefs anteriores **queda superada**. Atmósfera de campaña y pantallas de producto comparten ahora una sola paleta.

**Azul y teal quedan fuera de la película.** No existen como primitivas en el CSS. El spot se restringe a rojo, verde y ámbar sobre neutros: tres acentos semánticos leen con fuerza en 60 s; cinco leen como paleta decorativa.

**Punto de negro en rodaje.** El grado puede bajar por debajo de `#1a1b1e` si la fotografía lo pide. Eso es una decisión fotográfica, no un color de marca: no se usa para maquetar superficies ni se cita como corporativo. Los negros conservan detalle en todo caso.

### 5.2 Tipografía

- **Titulares y UI:** `Space Grotesk`, siempre en *sentence case*. Sin mayúsculas gritadas en los cartones narrativos.
- **Datos, criterios, sellos y registros:** `JetBrains Mono`. Es la voz del sistema; en la película distingue *lo que dice la marca* de *lo que registra el producto*.
- Regla de emisión: ningún rótulo por debajo de 28 px en master 4K; los datos monospace se leen, no se decoran.

### 5.3 Qué no aparece nunca en cámara

- Un perro en reactividad provocada. Ni ladrido, ni tensión de correa forzada, ni estímulo acercado para conseguir el plano.
- Golden retriever de catálogo, perro sonriente, cámara lenta feliz en campo dorado.
- Interfaces flotantes, holografía, destellos de IA, cerebro con circuitos, bocadillo de chat.
- Badges o pantallas de App Store / Google Play. **El producto es una aplicación web** y así está registrado en el registro de promesas.
- Huella de perro, cara frontal de perro, escudo, estética policial o táctica.
- Logotipos de clientes, testimonios, premios, cifras de usuarios o tasas de éxito. No existen.

---

## 6. Guardrails innegociables

1. **Ninguna promesa sobre el animal.** Ni «mejora», ni «lo resuelve», ni un antes/después. La certeza es del proceso.
2. **Ningún porcentaje como promesa.** El único número que aparece es el umbral de la regla, y se enuncia «por encima del 80 %», nunca «80 % o más». El umbral técnico es `successRate > 0.8`.
3. **La persona firma la decisión.** El profesional escribe la nota; el sistema registra. Si un plano sugiere que la IA decide sola, se cae del montaje.
4. **Vocabulario vetado:** curación, garantizado, infalible, diagnóstico, clínico, algoritmo que entiende a tu perro, resultados en X semanas.
5. **UI siempre rotulada** `DATOS DE DEMOSTRACIÓN` en las tomas de pantalla, como exigen los dos guiones de paid social.
6. **Bienestar sobre plano.** Si un plano solo funciona estresando al animal, el plano no existe. Sin excepción, sin «lo arreglamos en post».

---

## 7. Dos advertencias de encargo

Entregamos la pieza completa. Dos cosas hay que decirlas antes de que nadie firme un presupuesto:

**a) Mercado.** Todo el producto documentado es español: precios en euros, landings en español, investigación de mercado sobre el censo español, marco legal en la Ley 7/2023. La final de la NFL es una compra estadounidense. O bien la pausa de la NFL es aquí un **benchmark de ambición creativa** —la vara con la que medimos la pieza— o bien es una **entrada real al mercado de EE. UU.**, y entonces faltan investigación, catálogo, precios y encaje legal para ese mercado. El guion está construido para funcionar en los dos supuestos: [02](02-guion-spot-60s.md) incluye la versión en inglés de todas las líneas y rótulos.

**b) Readiness.** El registro de promesas mantiene abiertos, a fecha de corte: políticas legales enlazadas, banner de cookies, catálogo Stripe completo (solo hay un flujo Pro verificado), portal de facturación, verificación en producción de Consulta IA y **el clearance de marca de `K9 Architect`**, cuyo dominio figuraba sin registrar pero sin confirmar disponibilidad. Emitir en la mayor pausa publicitaria del mundo con el nombre sin registrar es el único riesgo de esta lista que no se puede arreglar después. Va primero.

Ninguna de las dos advertencias bloquea el trabajo creativo. Las dos bloquean la emisión.

---

## 8. Arquitectura de campaña

| Pieza | Duración | Uso | Fuente |
|---|---|---|---|
| **«Dos pasos atrás»** | 60 s | Master de emisión, 3.er cuarto | [02](02-guion-spot-60s.md) |
| **Cutdown de 30 s** | 30 s | Segunda emisión / digital premium | [02](02-guion-spot-60s.md) §4 |
| **Cutdown de 15 s** | 15 s | Social vertical 9:16, YouTube pre-roll | [02](02-guion-spot-60s.md) §5 |
| **Plano fijo de 6 s** | 6 s | Bumper, sin voz | Recorte de P09 |
| **Serie paid social** | 25–40 s ×16 | Ya guionizada, sin cambios | `campaigns/b2b|b2c/` |

Los cutdowns **no requieren rodaje ni generación adicional**: se remontan del material del master. Es coherente con una marca cuyo argumento es que el proceso ya registrado no debe rehacerse desde cero.
