# 05 · Exterior y gráfica estática

**Obligatoria para diseño gráfico, exterior y producción de impresión.**
Hermanos: [04 · Dirección de arte](04-direccion-de-arte.md) · [06 · Claims](06-claims-y-guardrails.md) · [07 · Especificaciones](07-entregables-y-especificaciones.md)

---

## 1. El problema que hay que resolver antes de bocetar

La identidad de K9 es **oscura** (`#1a1b1e`, fuente de verdad: `design-system/colors_and_type.css`). En pantalla es su mayor virtud. En exterior es su mayor riesgo, y no por gusto: por física.

| Soporte | Cómo se ilumina | Cómo se comporta el casi negro |
|---|---|---|
| **Marquesina / mupi** | **Retroiluminado** | ✅ Excelente. El fondo oscuro se vuelve profundo y los acentos brillan. Es el soporte natural de esta marca |
| **Pantalla LED / DOOH** | **Emisiva** | ✅ Excelente, con la reserva del brillo ambiental a pleno sol |
| **Valla, lona, monoposte** | **Reflejada, o sin luz de noche** | ❌ **Problema serio.** Ver §2 |
| **Cartel de metro, columna** | Ambiental interior | ⚠️ Aceptable con reservas |
| **Prensa, papel** | Reflejada | ❌ Malo |

### La regla que sale de aquí

> **Los soportes retroiluminados y emisivos usan el sistema oscuro de `colors_and_type.css`.**
> **Los soportes impresos y reflejados usan el sistema invertido en claro.**

No es una traición a la identidad. Es la misma identidad respondiendo a la luz que tiene delante — y el sistema ya contempla el modo claro (`--bg-page: #f3f4f6`, cards `#fefefe`).

---

## 2. Por qué el casi negro falla en una valla impresa

Cuatro razones acumulativas. Ninguna se arregla en arte final:

1. **El oscuro impreso no es `#1a1b1e`.** Sobre papel o lona, un negro plano de gran superficie se lee como gris sucio, con nubes y marcas de rodillo visibles a distancia media.
2. **La luz ambiental lo lava.** Una valla a mediodía recibe luz reflejada desde todas partes. El contraste real que llega al ojo es una fracción del contraste del archivo.
3. **De noche, una valla sin iluminar desaparece.** Un fondo casi negro no tiene nada que devolver.
4. **La ganancia de punto engorda la tipografía fina.** El texto claro sobre fondo oscuro pierde contraforma antes que el oscuro sobre claro. **JetBrains Mono en claro sobre negro es el peor caso posible** en gran formato.

### La versión impresa del sistema

| Elemento | Oscuro (retroiluminado) | **Claro (impreso)** |
|---|---|---|
| Fondo | `#1a1b1e` | `#f3f4f6` |
| Texto principal | `#f1f2f4` | `#111827` |
| Texto secundario | `#909399` | `#4b5563` |
| Superficie | `#25262b` | `#fefefe` |
| Borde | `#373a40` | `#e2e3e4` |
| Acentos | `#ef4444` `#10b981` `#f59e0b` | Los mismos, con la reserva de §6 |

La marca sigue siendo reconocible porque lo que la identifica no es el fondo: es **la pareja tipográfica, el rojo K9 y el rigor de la retícula.**

---

## 3. Cuánto tiempo tienes en cada soporte

Determina el número de palabras. No es una recomendación de estilo: es el diseño del soporte.

| Soporte | Tiempo real de lectura | Palabras máximo | Ideas por pieza |
|---|---|---:|---:|
| Valla en autovía | 1–2 s | **5** | 1 |
| Valla urbana, tráfico lento | 3–5 s | **8** | 1 |
| Marquesina, peatón esperando | 15–45 s | **25** | 1 principal + 1 apoyo |
| Mupi en calle, al pasar | 3–6 s | **8** | 1 |
| Cartel de andén de metro | 20–60 s | **35** | 1 principal + apoyo |
| DOOH con rotación de 10 s | 6–8 s útiles | **10** | 1 |

**La marquesina es el soporte estrella de esta marca.** Retroiluminada, con público quieto y con tiempo para leer un dato. Es el único formato de exterior donde el registro en JetBrains Mono —una decisión, un criterio, una distancia— puede funcionar de verdad.

**La valla es el soporte más hostil.** Cinco palabras y una idea. Si el concepto necesita explicación, no es un concepto de valla.

---

## 4. Tipografía en gran formato

### 4.1 Altura mínima de carácter

Regla de oficio: **unos 2,5 cm de altura de mayúscula por cada 10 m de distancia de lectura.** Se calcula desde el punto de visión real, no desde la ficha del soporte.

| Soporte | Distancia típica | Altura mínima de mayúscula |
|---|---|---|
| Valla 8 × 3 m en autovía | 100–150 m | **25–38 cm** |
| Valla urbana | 30–50 m | **8–13 cm** |
| Marquesina 120 × 175 cm | 1,5–4 m | **1–2 cm** |
| Mupi al paso | 5–10 m | **1,5–2,5 cm** |

### 4.2 Reglas duras

- **Space Grotesk para todo lo que se lee a distancia.** Titular, línea de marca, descriptor.
- **JetBrains Mono solo cuando hay tiempo de lectura**: marquesina, andén, DOOH con dwell. **Nunca** en una valla de autovía.
- **Suelo absoluto de mono:** si el dato no llega a la altura mínima de la tabla, **el dato se elimina**. No se reduce.
- **Sentence case** en titulares, siempre. ALL CAPS solo en etiquetas de estado en mono.
- **Interletrado abierto** en textos claros sobre fondo oscuro: compensa el engorde óptico.
- Máximo **dos pesos** por pieza. La jerarquía se hace con escala.

---

## 5. Composición

- **Una idea por superficie.** Si hay dos, hay dos piezas.
- **Retícula visible pero no decorada.** El rigor se nota en la alineación, no en líneas dibujadas.
- **Margen de seguridad del 10 %** del lado menor. Ningún elemento crítico dentro de él.
- **Nada a sangre detrás de texto.** Sin fotos de fondo bajo un titular.
- **El logotipo tiene su esquina y no compite.** Nunca centrado bajo el titular como una firma de cartel de cine.
- **Espacio vacío es un activo**, no un error de maquetación. En una calle saturada, el vacío es lo que hace girar la cabeza.

---

## 6. Producción de impresión

### 6.1 Los acentos de marca están fuera de gama CMYK

Aviso importante para arte final: **`#ef4444` y `#10b981` son colores RGB brillantes que se apagan al convertir a CMYK.** El verde esmeralda es especialmente problemático: pierde saturación y vira a un verde apagado.

**Procedimiento obligatorio:**

1. Convertir bajo el perfil real de producción, acordado con el impresor.
2. **Prueba de color contractual antes de producir.** No se aprueba en pantalla.
3. Si el rojo K9 es crítico en un soporte concreto, valorar **tinta directa Pantone** en lugar de cuatricromía, y fijar la equivalencia de una vez para toda la campaña.
4. Registrar las equivalencias aprobadas en el manual y no volver a decidirlas por pieza.

### 6.2 Negro rico

Si una pieza usa fondo oscuro impreso, **nunca 100 % K solo**. Punto de partida a validar con el impresor: `C40 M30 Y30 K100` para grandes superficies. Con negro plano se obtiene un gris lavado con nubes.

### 6.3 Resolución y archivos

- Gran formato: arte a **escala 1:10 a 300 ppp**, o escala real a 30 ppp. Se acuerda con el proveedor antes de empezar.
- **Sangre y marcas** según ficha técnica de cada soporte.
- Tipografías **convertidas a contornos**.
- PDF/X según lo que pida la imprenta.
- **La tipografía del logotipo se entrega trazada.** El SVG de la propuesta actual referencia una fuente por ruta relativa; no sirve para producción.

### 6.4 Contraste y accesibilidad

Contraste mínimo 4,5:1 para texto secundario y 3:1 para texto grande, verificado sobre el color final impreso, no sobre el hex de pantalla. **El sentido nunca depende solo del color:** si el verde significa criterio cumplido, hay una palabra que también lo dice.

---

## 7. QR y llamadas a la acción

- **Valla y autovía: sin QR.** Nadie escanea a 90 km/h. Y una URL larga tampoco se lee.
- **Marquesina, andén, mupi con dwell: QR sí**, con zona de silencio propia, tamaño suficiente para escanear a un metro, y **destino con UTM propio del soporte** para poder medir.
- La URL, cuando aparece, va en **Space Grotesk**, no en mono, y sin `https://` ni `www`.
- **Ninguna pieza de exterior menciona precio ni condiciones de prueba** sin autorización expresa. Ver [06 · §5](06-claims-y-guardrails.md).

---

## 8. Formatos de referencia

| Formato | Medida orientativa | Sistema | Notas |
|---|---|---|---|
| Valla / cartelera | 8 × 3 m | **Claro** | 5–8 palabras. Sin QR |
| Monoposte | Variable, gran distancia | **Claro** | 5 palabras |
| Lona de fachada | Variable | **Claro** | Cuidado con dobleces y perforación |
| Marquesina | 120 × 175 cm | **Oscuro** (retro) | Formato estrella. Admite un dato |
| Mupi calle | 120 × 175 cm | Según retroiluminación | Verificar soporte antes de decidir |
| Cartel de metro | 4 × 3 m / 3 × 1,5 m | Según iluminación del andén | Admite lectura larga |
| DOOH / LED | Según red | **Oscuro** | Contraste alto por brillo ambiental |
| Cabecera digital | Según red | **Oscuro** | Sin sonido, sin dependencia de audio |

**Confirmar siempre la ficha técnica real del soporte contratado antes de maquetar.** Las medidas varían por operador y por país.

---

## 9. Gráfica estática digital

Para display, social estático y cabeceras, el sistema oscuro es el que manda. Dimensiones en [07](07-entregables-y-especificaciones.md).

Reglas propias:

- **Se entiende sin contexto.** Una pieza estática no tiene 20 segundos para explicarse.
- **Texto dentro del 80 % central** en formatos de social vertical.
- **Ninguna pantalla de producto sin `DATOS DE DEMOSTRACIÓN`.**
- El mismo concepto debe existir en horizontal, cuadrado y vertical **recompuesto**, no recortado.

---

## 10. Checklist antes de mandar a producción

- [ ] ¿El soporte es retroiluminado? Si no, ¿está en sistema claro?
- [ ] ¿El número de palabras cabe en el tiempo real de lectura?
- [ ] ¿Hay **una** sola idea?
- [ ] ¿La altura de mayúscula supera el mínimo para la distancia real?
- [ ] ¿Hay mono por debajo del suelo de legibilidad? Elimínalo.
- [ ] ¿Prueba de color contractual aprobada?
- [ ] ¿Negro rico, no 100 % K?
- [ ] ¿Tipografías trazadas?
- [ ] ¿Contraste verificado sobre el color impreso final?
- [ ] ¿QR solo donde hay dwell, con UTM propio?
- [ ] ¿Sin precios, sin promesas de resultado, sin badges de tienda?
- [ ] ¿Logotipo aprobado por el cliente? *(Ver [09 · D1](09-decisiones-abiertas.md) — hoy está abierto)*
