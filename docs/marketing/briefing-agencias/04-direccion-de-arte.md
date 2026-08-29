# 04 · Dirección de arte y sistema visual

**Obligatoria para arte, diseño, fotografía, dirección de fotografía y motion.**
Hermanos: [01 · Plataforma](01-plataforma-de-marca.md) · [05 · Exterior](05-exterior-y-grafica-estatica.md) · [07 · Especificaciones](07-entregables-y-especificaciones.md) · [09 · Decisiones abiertas](09-decisiones-abiertas.md)

**Fuente técnica:** `design-system/colors_and_type.css`, `design-system/CLAUDE.md`, `design-system/assets/`, `design-system/proposals/`.

---

## 1. El principio rector

> **Oscuro, estructurado y preciso.** Un sistema de control y de rigor, no un producto de consumo.

Todo lo demás se deriva de ahí. Si una decisión visual hace que K9 parezca simpático, aspiracional o mágico, es una decisión equivocada aunque sea bonita.

---

## 2. Color

### 2.1 Los tres acentos semánticos

Son **semánticos, no decorativos**. Cada uno significa algo concreto en el producto y ese significado se respeta también en publicidad.

| Color | Hex | Significa | **No** significa |
|---|---|---|---|
| **Rojo K9** | `#ef4444` | Acción, marca, pausa, señal clara | Peligro barato, urgencia, alarma |
| **Verde criterio** | `#10b981` | **Criterio cumplido** | Éxito del perro, victoria, felicidad |
| **Ámbar** | `#f59e0b` | Atención, observar, revisar | Advertencia dramática |

Usar el verde para celebrar a un perro, o el rojo para asustar, rompe el sistema. En una marca cuyo argumento es el rigor, eso se nota.

### 2.2 Los neutros — fuente de verdad

**`design-system/colors_and_type.css` es la fuente de verdad de la paleta.** Decisión cerrada. Cualquier otra escala que aparezca en documentos anteriores queda superada.

| Rol | Token | Hex |
|---|---|---|
| Fondo de página | `--bg-page` | `#1a1b1e` |
| Superficie / card | `--bg-card` | `#25262b` |
| Sidebar | `--bg-sidebar` | `#1e1f24` |
| Borde sutil | `--border-subtle` | `#373a40` |
| Borde por defecto | `--border-default` | `#4c4f56` |

**Consecuencia para producción:** la atmósfera de campaña y las pantallas de producto usan **la misma escala**. Ya no hay dos sistemas que reconciliar, y un anuncio que enseñe la interfaz coincidirá con lo que ve un usuario real.

**Punto de negro en rodaje.** Un grado cinematográfico puede bajar por debajo de `#1a1b1e` — es una decisión fotográfica, no un token de marca. Lo que no puede hacerse es presentar ese negro como color corporativo ni usarlo para maquetar superficies. Los negros conservan detalle: penumbra, no aplastamiento.
### 2.3 Azul, teal y morado

`design-system/CLAUDE.md` documenta superposiciones de tarjeta en azul `#3b82f6`, teal `#14b8a6` y morado `#8b5cf6`. **Ninguno de los tres está definido como primitiva en `colors_and_type.css`**, cuyas escalas son rojo, verde, naranja, gris y slate.

**Decisión para comunicación: fuera.** La publicidad de K9 se restringe a **rojo, verde, ámbar y neutros**. Tres acentos semánticos leen con fuerza; cinco leen como paleta decorativa, que es exactamente lo que el posicionamiento prohíbe.

### 2.4 Neutros de texto

```text
--text-primary     #f1f2f4
--text-secondary   #c1c2c5
--text-muted       #909399
--text-disabled    #636670
```

### 2.5 Modo claro

Existe y está soportado (`--bg-page: #f3f4f6`, cards `#fefefe`). **No es el modo por defecto de la marca**, pero es obligatorio para exterior impreso. Ver [05](05-exterior-y-grafica-estatica.md).

---

## 3. Tipografía

| Papel | Fuente | Uso |
|---|---|---|
| **Titulares, UI, cuerpo** | **Space Grotesk** | Todo el texto de marca |
| **Datos, criterios, sellos, registros** | **JetBrains Mono** | Cifras, tiempos, distancias, estados, IDs |

Pesos disponibles en local: Space Grotesk 300–700; JetBrains Mono 100–800 con itálicas.

### 3.1 La regla que hace funcionar el sistema

> **Space Grotesk es la voz de la marca. JetBrains Mono es la voz del sistema.**

Un titular en mono suena a que lo dice la máquina. Un dato en Space Grotesk pierde la textura de registro. La tensión entre las dos voces **es** la identidad. Se respeta.

### 3.2 Casing — ⚠️ inconsistencia documentada

`design-system/README.md` prescribe **Title Case** para navegación y titulares, voz «clínica» y «English-first». La plataforma de marca y el registro de claims prescriben **sentence case**, español primero, y **vetan expresamente la palabra «clínico»** por riesgo jurídico.

**Resolución acordada en la reunión:**

- **Comunicación y publicidad: sentence case, español, y nunca «clínico».** Manda [01](01-plataforma-de-marca.md).
- El README del design system describe la **interfaz del producto** tal como se especificó originalmente y queda pendiente de armonización. No gobierna la publicidad.
- **ALL CAPS** se reserva a etiquetas de estado en mono (`ATENCIÓN`, `DATOS DE DEMOSTRACIÓN`). Nunca a titulares.

### 3.3 Escala

La escala del producto es densa (11–36 px). **No sirve para publicidad.** Para campaña se construye una escala editorial propia con la misma familia, con contraste de tamaño alto: la jerarquía se hace con escala y espacio, nunca con cinco pesos distintos en la misma pieza.

---

## 4. Logotipo

### 4.1 Estado: resuelto en dirección, abierto en elección

La huella roja que había en producción **ha sido retirada**. La identidad es ahora un **wordmark sin glifo**, coherente con la dirección aprobada en la auditoría de naming y logo.

`design-system/assets/K9 Architect logo options/`

### 4.2 La construcción

`K` en color de texto principal, **`9` en rojo K9 `#ef4444`**, seguido de «Architect». El rojo no decora: identifica. Es el único elemento de color de la marca.

Dos lockups en evaluación:

| Opción | Construcción |
|---|---|
| **1A · inline** | `K9` en bold y `Architect` en light, sobre una misma línea de base. Contraste por peso |
| **1B · apilado** | `K9` en bold sobre `ARCHITECT` en JetBrains Mono con interletrado muy abierto |

**Marca cuadrada** para icono de aplicación, favicon y avatar: **solo tipografía**, `K9` dentro de un cuadrado de esquinas redondeadas. Sin símbolo.

### 4.3 Qué está cerrado y qué no

- ✅ **Cerrado:** sin glifo, sin huella, sin símbolo. Wordmark tipográfico.
- ✅ **Cerrado:** el `9` va en rojo K9. La `K` en neutro.
- ⏳ **Abierto:** elegir entre 1A y 1B. Es decisión del cliente. Ver [09 · D1](09-decisiones-abiertas.md).

**Cómo trabajar:** se puede conceptar y maquetar con cualquiera de las dos. **No se cierra arte final** hasta que el cliente elija. **Nadie diseña un logotipo nuevo** dentro de un lote de campaña.

### 4.4 Prohibido en cualquier marca, icono o ilustración

Huella · cara frontal de perro · silueta de raza · perro dentro de escudo · estética policial o táctica · cerebro con circuitos · robot · destello de IA · bocadillo de chat.

**Un solo logotipo para dueños y profesionales.** No hay versión Pro.

### 4.5 Requisitos de validación de la marca elegida

Icono a 1024 px y a 32 px · favicon 16 y 32 px · cabecera de landing escritorio y móvil · sidebar de producto · avatar circular · una tinta · blanco sobre negro · negro sobre blanco · lectura de cinco segundos con y sin descriptor.

**Para producción:** la tipografía del wordmark se entrega **trazada a contornos**. Ningún archivo de marca puede depender de una fuente por ruta externa.
---

## 5. Fotografía y casting

### 5.1 Personas

Personas reales, no modelos. Ropa cotidiana, no técnica ni deportiva. Caras con historia. Manos que trabajan.

**Dirección de actores, en una frase:** *no interpretes alivio; interpreta que acabas de entender algo.* La emoción de esta marca es la comprensión, no la felicidad.

**Nunca:** sonrisa a cámara, pulgar arriba, salto de celebración, abrazo al perro en cámara lenta.

### 5.2 Perros

- **Mestizos de tamaño medio**, pelo corto o semilargo, marcas asimétricas, orejas expresivas.
- **Nunca** raza reconocible de catálogo. Nunca golden retriever. Nunca cachorro como gancho.
- **Perros tranquilos y entrenados que interpretan atención**, no perros reactivos reales.
- Sin collar de castigo, de púas ni eléctrico. Collar plano o arnés de bienestar.
- Correa **siempre floja** salvo que el guion exija lo contrario y esté aprobado.

### 5.3 La restricción central, y por qué es una ventaja

> **Se puede hacer una campaña entera sobre reactividad canina sin mostrar ni un solo perro reactivo.**

La tensión se cuenta en la persona: la mano que se cierra sobre la correa, la mandíbula, la mirada que calcula distancia. Todo el mundo ha visto un perro ladrando; casi nadie ha visto contada la parte que le duele al dueño.

No es solo una concesión de bienestar. Es el mejor territorio de imagen disponible.

### 5.4 Entornos

Interiores en penumbra natural con texturas reales. Exteriores creíbles de trabajo canino al amanecer o al atardecer. Despachos pequeños con libros gastados y cables a la vista.

**Nunca:** plató clínico, bata blanca, pared de diplomas, mesa de showroom, planta decorativa, oficina de startup.

---

## 6. Dirección de fotografía

| Parámetro | Especificación |
|---|---|
| **Look** | Naturalista de baja intensidad, claroscuro sobrio y volumétrico |
| **Punto de negro** | Puede bajar por debajo de `#1a1b1e` si el grado lo pide: es decisión fotográfica, no token de marca. **Siempre conservando detalle.** Penumbra, no aplastamiento |
| **Paleta en cámara** | Desaturada. Grises fríos y marrones apagados. El único color saturado en cuadro es un acento de marca justificado |
| **Grano** | Presente y honesto. Emulación de película. Nunca limpieza digital de catálogo |
| **Óptica** | Anamórfico limpio. **Sin flare azul decorativo** |
| **Movimiento** | **Solo dolly y plano fijo.** Prohibidos: dron, FPV, steadicam nerviosa, whip-pan, zoom digital, rampas de velocidad |
| **Iluminación** | Fuente única direccional más rebote. Luz práctica cuando exista: ventana, farola, el propio panel de una pantalla |

**Prohibido el degradado teal-naranja.** Es la firma visual de la publicidad genérica y contradice todo lo anterior.

---

## 7. Pantallas de producto en cámara

**Regla técnica de producción, no estética.**

Las pantallas **no se ruedan en vivo y no se generan con IA**. Se ruedan con el dispositivo apagado o con carta gris, y la interfaz se compone en posproducción sobre marcadores de seguimiento, a partir de renders exactos construidos con los tokens del producto.

Razones: legibilidad garantizada en emisión, tipografía correcta, datos de demostración controlados, cero riesgo de filtrar datos reales y cero riesgo de que aparezca en pantalla un texto inventado — que sería un claim no verificado.

**Obligatorio en toda toma de interfaz:**

- Rótulo `DATOS DE DEMOSTRACIÓN`, mono, `#909399`, arriba a la derecha.
- Ningún dato personal real, incluidas barra de navegación, notificaciones del sistema y nombres de archivo.
- Rebote de luz de pantalla añadido en composición sobre manos y rostro, o el plano delata el truco.

---

## 8. Iconografía

Iconos de trazo minimalista, familia Lucide o equivalente, grosor 1,5 px. Sin relleno, sin degradado, sin emoji.

**Prohibidos:** huella, cara de perro, hueso, cerebro, robot, chispa de IA, bocadillo de chat.

---

## 9. Composición y layout

- **Radio de esquina 8 px** en tarjetas y contenedores. Es el radio del sistema.
- **Bordes de 1 px uniformes.** ⚠️ Regla explícita del design system: **prohibido el borde grueso de acento a la izquierda o arriba** (`border-left: 3px solid`). Para dar color a una superficie: borde de 1 px al 35 % de opacidad más fondo al 7 %.
- **Dos niveles de profundidad**: la página es más oscura que la tarjeta. Sombra muy baja o ninguna.
- **Sin degradados de fondo. Sin imágenes a sangre detrás de texto. Superficies planas y limpias.**
- La jerarquía se construye con **escala y espacio**, no con peso ni con color.

---

## 10. Movimiento y motion graphics

- Transiciones funcionales, ~150 ms, curva suave. **Nada elástico ni rebotante.**
- Se animan `transform` y `opacity`. No se anima layout.
- Los datos aparecen; no se cuentan hacia arriba como un marcador.
- **Ningún efecto sugiere que la IA «piensa»**: sin partículas, sin pulsos, sin barrido de escáner, sin ondas.
- El sonido de interfaz, si existe, es un háptico o un tono grave apenas audible. Nunca un *ding* de éxito.

---

## 11. Los diez errores que rechazaremos sin discusión

1. Huella de perro en cualquier forma.
2. Interfaz holográfica o flotante.
3. Degradado morado o azul de «tecnología».
4. Verde usado como celebración en vez de como criterio cumplido.
5. Rojo usado como alarma en vez de como acción o pausa.
6. Title Case en titulares.
7. Borde grueso de acento lateral o superior.
8. Perro reactivo en cámara.
9. Badge de App Store o Google Play.
10. Una pantalla de producto que no existe.
