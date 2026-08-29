# YouTube España + Europa — Territorios creativos y guiones

**Hermanos:** [01 · Visión](01-vision-y-estrategia.md) · [03 · Arquitectura YouTube](03-arquitectura-youtube.md) · [04 · Clearance](04-clearance-y-bloqueantes.md)

---

## 0. Las reglas de producción de este emplazamiento

Antes de cualquier guion, las cinco restricciones que hacen que una pieza funcione delante de este público:

1. **La idea entera vive en los primeros 5 segundos.** En in-stream saltable, el segundo 5 es el único momento garantizado. La pieza debe haber dicho algo completo antes de que aparezca el botón. Los 15 siguientes son la prueba, no el desarrollo.
2. **Pantalla primero, persona después.** El primer fotograma es producto o dato, nunca un plano de un perro corriendo. Un perro en el segundo 1 es indistinguible de un anuncio de pienso y se salta.
3. **Sin música en los primeros 5 segundos.** La música es la señal más rápida de «esto es publicidad». Entra después, si entra.
4. **Voz de profesional, no de locutor.** Grabada como se le explica algo a un colega, con la sala audible. Nada de cabina, nada de sonrisa en la voz.
5. **Todo se entiende sin sonido.** Subtítulos quemados, revisados a mano, dos líneas máximo. Buena parte del consumo de YouTube en móvil y en oficina es silencioso.

**Sistema visual** (`design-system/colors_and_type.css`): fondo `#1a1b1e`, superficies `#25262b`, bordes `#373a40` — **el CSS es la fuente de verdad**. Rojo `#ef4444` acción y pausa; verde `#10b981` criterio cumplido; ámbar `#f59e0b` atención. Space Grotesk en titulares y sentence case; JetBrains Mono en datos y criterios. Rótulo `DATOS DE DEMOSTRACIÓN` visible en toda toma de interfaz.

---

# Territorio A · «Júzgalo por lo que se niega a hacer»

**Audiencia:** profesional. **Uso:** in-stream saltable + bumper. **Función:** derribar la objeción PRO-11 antes de vender nada.

La serie enseña los tres mecanismos de restricción del producto. Los tres constan como verificados en código y pruebas. Ninguna otra empresa de la categoría puede rodar estos anuncios.

---

## A1 · El veto — 20 s

**Hipótesis:** enseñar a la IA siendo rechazada genera más confianza profesional que enseñarla acertando.

| TC | Imagen | Voz | Texto en pantalla |
|---:|---|---|---|
| 0:00–0:02 | Negro medio segundo. Entra de golpe una tarjeta de interfaz sobre `#1a1b1e`, con borde ámbar. Sin música. | — | `Plan rechazado — revisión de bienestar` |
| 0:02–0:05 | La tarjeta se mantiene. Debajo aparece el motivo, en mono. | «Este plan lo ha generado nuestra IA. Y nuestro propio sistema lo ha rechazado.» | `Motivo: exposición por encima del umbral seguro para la edad` |
| 0:05–0:10 | Corte a la profesional, plano medio, despacho real, luz de ventana. Habla mirando la pantalla, no a cámara. | «Un generador que nunca dice que no, no es una herramienta. Es un riesgo con buena interfaz.» | — |
| 0:10–0:16 | Vuelta a pantalla. El plan corregido aparece con el paso reducido. El acento pasa de ámbar a neutro. Sigue sin música. | «En K9 cada plan pasa por una revisión de bienestar que puede vetarlo. Y tú revisas lo que queda.» | `Revisión de bienestar · Ajuste profesional · Auditoría` |
| 0:16–0:20 | End card sobrio. Entra una única nota grave. | «Júzgalo por lo que se niega a hacer.» | `K9 ARCHITECT` · `Del caso al informe.` · `Aplicación web` |

**CTA:** Ver el recorrido completo → activo largo B1.

**Nota de precisión:** los rótulos `Plan rechazado — revisión de bienestar` y el texto de motivo **deben reproducir literalmente lo que muestra el producto**. Si el veto no tiene hoy una pantalla con ese texto, se construye la pantalla antes de rodar el anuncio, no al revés. Ver [04 · §1](04-clearance-y-bloqueantes.md).

---

## A2 · La pausa — 20 s

**Hipótesis:** el miedo del profesional a que el dueño empeore el caso en casa pesa más que cualquier ganancia de eficiencia.

| TC | Imagen | Voz | Texto en pantalla |
|---:|---|---|---|
| 0:00–0:02 | Interfaz. Un plan activo, en marcha. De pronto, banda roja. | — | `Plan en pausa` |
| 0:02–0:05 | El motivo aparece debajo, en mono. | «El dueño reportó un incidente. El plan se ha detenido solo.» | `Incidente reportado en sesión · derivación recomendada` |
| 0:05–0:11 | Profesional, plano medio. | «Lo que me quitaba el sueño no era que el cliente no practicase. Era que practicase mal un martes y yo me enterase el jueves.» | — |
| 0:11–0:17 | Ficha del caso: la señal ha subido al panel de atención en ámbar. Cursor sobre ella. | «El incidente detiene el paso y sube al panel. La decisión de qué hacer sigue siendo tuya.» | `ATENCIÓN · incidente reportado` |
| 0:17–0:20 | End card. | «Júzgalo por lo que se niega a hacer.» | `K9 ARCHITECT` · `Del caso al informe.` |

**Guardrail:** no dramatizar el incidente. No se muestra, no se describe, no se recrea. Solo existe como registro en pantalla. La pieza habla de la respuesta del sistema, nunca del suceso.

---

## A3 · La derivación — 20 s · **CONDICIONAL**

**Estado:** Consulta IA figura como *IMPLEMENTADO / VERIFICAR PRODUCCIÓN* en ambos roles. **No se produce hasta cerrar esa verificación.** Además, en la UE activa obligaciones de transparencia del artículo 50 del AI Act. Ver [04 · §2](04-clearance-y-bloqueantes.md).

| TC | Imagen | Voz | Texto en pantalla |
|---:|---|---|---|
| 0:00–0:03 | Campo de consulta. Se escribe una pregunta con señal de riesgo. En vez de responder, el sistema se detiene. | — | `Esta consulta no se responde aquí.` |
| 0:03–0:06 | Aparece la ruta de derivación. | «Le hemos preguntado algo que no debía contestar. Y no lo ha contestado.» | `Recomendación: valoración veterinaria` |
| 0:06–0:13 | Profesional. | «Puedo convivir con una herramienta que a veces no sabe. No puedo convivir con una que siempre responde.» | — |
| 0:13–0:17 | Interfaz: respuesta normal con sus fuentes visibles. | «Cuando responde, enseña de dónde. Y no toca tu plan.» | `Fuentes · No modifica el plan` |
| 0:17–0:20 | End card + aviso obligatorio de IA. | — | `Consulta IA es un sistema de IA.` |

---

## A4 · Bumper de 6 s · no saltable

Una idea, sin voz, sin música. Se usa para frecuencia y memoria sobre la misma lista blanca.

```text
0:00–0:04   Tarjeta sobre negro, borde ámbar:
            Plan rechazado — revisión de bienestar

0:04–0:06   K9 ARCHITECT
            Júzgalo por lo que se niega a hacer.
```

Variante B: sustituir la tarjeta por `Plan en pausa`. Variante C: `Esta consulta no se responde aquí.` (condicionada como A3).

---

# Territorio B · «El caso entero, sin cortes»

**Audiencia:** profesional en consideración. **Uso:** activo largo orgánico + una pieza de pago que lo siembra. **Función:** convertir. Es el activo de la campaña.

---

## B1 · El activo largo — 6 a 8 minutos

**Formato:** grabación de pantalla continua, sin cortes de montaje, con voz en directo. Cámara de la persona en una esquina, pequeña. Sin música, sin gráficos, sin intro animada.

**Por qué así:** un profesional escéptico no cree un vídeo montado. Cree un vídeo donde algo sale mal y no se ha cortado. Es la única forma de credibilidad disponible para una empresa sin prueba social, y es exactamente coherente con la voz de marca.

**Estructura:**

| Bloque | Contenido | Duración |
|---|---|---|
| 1 | Se enuncia el caso compuesto en voz alta y se escribe en el formulario, dudas incluidas. | ~1 min |
| 2 | Se revisa el resumen que entra al motor **antes** de generar. Se corrige algo. | ~1 min |
| 3 | Se genera. Se espera en tiempo real. Se lee el plan **con sus limitaciones**. | ~1,5 min |
| 4 | **El bloque que hace único al vídeo:** una sesión sale mal. Se reporta 2/5 con señales. El motor decide reducir una dimensión. Se explica por qué eso es correcto y no un fallo. | ~2 min |
| 5 | Ajuste profesional dentro del rango permitido, nota en el paso, rastro de auditoría. Se dice en voz alta **qué no se puede editar y por qué**. | ~1 min |
| 6 | Informe PDF generado desde lo ya registrado. Se dice que lleva **el nombre del negocio en texto**, no un logotipo. | ~45 s |
| 7 | Cierre honesto: lista hablada de lo que K9 **no** hace hoy. | ~45 s |

**El bloque 7 no es una concesión: es el argumento de venta.** Decir en voz alta que no hay app de tienda, ni sincronización de calendario, ni logotipo en el informe, ni equipos, hace creíble todo lo anterior ante un público que ha visto cien demos infladas.

**Obligatorio:** caso **compuesto o anonimizado con autorización verificable**, rótulo `DATOS DE DEMOSTRACIÓN` permanente, y ninguna imagen de cliente o perro real sin consentimiento específico.

**SEO del activo:** título y descripción escritos para búsqueda profesional real, no para la marca. El clúster de vocabulario ya está definido en la estrategia de contenidos vigente (`estrategia-contenidos-redes-sociales-2026-08-22.md`, §12) y se reutiliza tal cual.

---

## B2 · La siembra — 45 s in-stream

Lleva tráfico cualificado a B1. No intenta cerrar la venta.

| TC | Imagen | Voz | Texto |
|---:|---|---|---|
| 0:00–0:05 | Grabación de pantalla en marcha, ya empezada, con el cursor moviéndose. Sensación de entrar a mitad de algo. | «Hemos grabado un caso entero sin cortar nada. Incluida la sesión que sale mal.» | `Sin cortes` |
| 0:05–0:15 | Recorrido rápido: caso → plan → sesión fallida → decisión de reducir. | «Se describe el caso. Se genera el programa. Se practica. Sale 2 de 5.» | `2/5 · señales: jadeo` |
| 0:15–0:28 | La decisión en pantalla. | «Y el sistema no insiste: reduce la distancia y deja el resto igual. Una dificultad cada vez.» | `REDUCIR UNA DIMENSIÓN · 8 m → 12 m` |
| 0:28–0:40 | Panel del profesional, nota, auditoría, informe. | «Lo que el dueño reporta llega al caso. El informe sale de ahí. Tú decides qué hacer con todo eso.» | `Práctica reportada · Nota · Informe` |
| 0:40–0:45 | End card con CTA explícito al vídeo largo. | «Está entero en el canal. Dura seis minutos y no hemos quitado nada.» | `Ver el caso completo` |

---

# Territorio C · «No siempre te va a dar un ejercicio»

**Audiencia:** dueño. **Uso:** Shorts verticales y remanente de la misma lista blanca. **Función:** volumen barato, no prioridad.

Se apoya en una pieza ya guionizada y aprobada de la campaña B2C —C05, «Saber parar también es cuidar»— para no abrir un territorio nuevo sin necesidad.

## C1 · Short vertical — 25 s · 9:16

| TC | Imagen | Voz | Texto |
|---:|---|---|---|
| 0:00–0:03 | Persona a cámara, entorno doméstico real, sin producción. | «Una aplicación responsable no siempre debería darte otro ejercicio.» | `A VECES DEBE DECIR: PARA` |
| 0:03–0:09 | Pantalla: el plan se detiene y aparece la ruta de ayuda. | «A veces la respuesta correcta es parar y buscar ayuda.» | `PAUSA Y DERIVACIÓN` |
| 0:09–0:16 | Pantalla: reporte y decisión de facilitar. | «Y cuando sí sigue, usa lo que pasó ayer para decidir lo de hoy.» | `REPORTE → SIGUIENTE AJUSTE` |
| 0:16–0:21 | Persona, plano quieto. | «Facilitar un paso no es que tu perro haya fallado.» | `NO ES UNA GARANTÍA` |
| 0:21–0:25 | End card B2C vigente. | «Un paso cada vez.» | `K9 ARCHITECT` · `Un paso cada vez.` · `Aplicación web` |

**Guardrail heredado sin cambios:** si hay riesgo inmediato, no se dirige a autoservicio. La pieza termina en información, no en registro.

## C2 · Bumper 6 s

```text
0:00–0:04   Tarjeta:  A veces la respuesta correcta es: para.
0:04–0:06   K9 ARCHITECT · Un paso cada vez.
```

---

# Territorio D · Programa de profesionales piloto

No es publicidad. Es la jugada estructural de [01 · §5](01-vision-y-estrategia.md) y produce los activos que el dinero no compra.

| Pieza | Qué es | Quién la publica |
|---|---|---|
| **D1 · Caso llevado en abierto** | Un profesional del programa lleva un caso real en K9 durante 6–8 semanas y lo cuenta en su canal, con su formato y su criterio. | El profesional |
| **D2 · Crítica sin guion** | Un profesional respetado usa el producto y dice en cámara **qué le sobra y qué le falta**, sin aprobación previa de K9. | El profesional |
| **D3 · Conversación de método** | Entrevista larga sobre progresión, umbrales y criterios. El producto aparece como contexto, no como tema. | Canal propio de K9 |

**Condiciones innegociables del programa:**

- **Sin aprobación editorial previa.** Si K9 revisa el guion, el activo pierde su único valor. Se acepta el riesgo de una crítica pública: es más barato que la desconfianza.
- **Divulgación de la relación comercial** clara y visible, según normativa de publicidad ES/UE y las propias reglas de YouTube.
- **Consentimiento verificable** de dueño y perro para cualquier caso real.
- **Selección por método, no por audiencia.** Un canal grande de enfoque aversivo no entra ni con descuento. Ver [01 · §6](01-vision-y-estrategia.md).
- El profesional conserva su criterio y puede discrepar del sistema en cámara. Eso es contenido, no un incidente.

---

## Prioridad de producción

| Orden | Pieza | Por qué en ese lugar |
|---:|---|---|
| 1 | **B1** activo largo | Es el destino de todo el pago. Sin él, la campaña compra visitas a un sitio vacío. |
| 2 | **A1** el veto | La creatividad de test principal, la que valida o tumba la hipótesis entera. |
| 3 | **B2** siembra | Sin ella, B1 no recibe tráfico. |
| 4 | **A2** la pausa | Segunda variante de la hipótesis. Necesaria para no saturar una lista blanca pequeña. |
| 5 | **A4 / C2** bumpers | Baratos, se derivan del material ya producido. |
| 6 | **C1** Short B2C | Remanente. |
| 7 | **A3** la derivación | **Bloqueado** hasta verificar Consulta IA en producción y cerrar el aviso del AI Act. |

D1–D3 corren en paralelo desde la semana uno: se negocian lento.
