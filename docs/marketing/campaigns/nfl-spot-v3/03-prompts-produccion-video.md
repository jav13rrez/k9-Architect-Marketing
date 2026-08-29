# «Dos pasos atrás» — Prompts de producción de vídeo

**Motores objetivo:** Sora · Runway Gen-3/Gen-4 · Kling
**Documentos hermanos:** [01 · Brief estratégico](01-brief-estrategico.md) · [02 · Guion 60 s](02-guion-spot-60s.md) · [04 · Clearance de claims](04-clearance-de-claims.md)

Diez prompts que cubren el máster completo. Cada uno lleva los cinco bloques obligatorios más su cadena en inglés lista para pegar. Los cutdowns se remontan de este material: no hay prompts adicionales.

---

## Reglas de uso antes del primer render

### R1 · Ninguna pantalla se genera

Los planos P05 y P08 son **planos de placa**: el móvil y el portátil se generan con la pantalla **apagada, en negro o con una carta gris uniforme**, y la interfaz se compone después en post sobre los renders exactos de UI.

Ningún motor generativo produce hoy tipografía legible y estable. Pedir `Space Grotesk` con datos correctos a un modelo de vídeo devuelve texto inventado, y ese texto sería un claim no verificado emitido ante cien millones de personas. Las cadenas de P05 y P08 incluyen la instrucción de pantalla apagada de forma explícita.

### R2 · Un motivo, tres condiciones de luz

P01, P09 y P10 comparten **exactamente el mismo encuadre**. En generación eso no se consigue repitiendo el prompt: se consigue generando P01 primero y usándolo como imagen de referencia o primer fotograma de las variantes, cambiando solo la descripción de luz y clima. Si el motor disponible no admite referencia de imagen, estos tres planos se ruedan; el dispositivo formal de la película depende de que el encuadre sea idéntico.

### R3 · Continuidad de sujeto

La misma mujer aparece en P01, P04, P06, P09 y P10; el mismo perro en siete de los diez planos. La deriva de identidad entre clips es el fallo más caro de este montaje. Fijar una descripción canónica de reparto —abajo— y repetirla **palabra por palabra** en cada cadena; generar todos los planos de un mismo sujeto en la misma sesión y con la misma semilla siempre que el motor lo permita.

```text
CANON — MUJER
early-forties woman, shoulder-length dark brown hair loosely tied back,
pale skin, no makeup, charcoal wool coat over a grey sweater, black gloves,
tired attentive face, no jewellery

CANON — PERRO
medium-sized mixed-breed dog, roughly 20 kg, short brindle and white coat
with an irregular white patch on the chest, upright expressive ears,
dark eyes, plain flat black biothane collar, no harness, no tags

CANON — PROFESIONAL
woman in her mid-forties, short greying hair, dark navy sweater,
no lab coat, reading glasses pushed up, working hands
```

### R4 · Longitud y montaje

Generar en clips de 5–8 s. Ningún plano del máster supera los 6 s salvo P10. Generar cada plano con 2 s de margen por delante y por detrás para tener sitio donde cortar.

### R5 · Ratio

Generar en el ratio nativo más ancho que ofrezca el motor y recortar a 2.39:1 en post. No pedir 2.39:1 al motor: suele interpretarse como recorte del contenido, no del encuadre, y se pierde cabeza.

### R6 · Bloque de exclusiones común

Estas exclusiones se repiten en los diez prompts porque describen la marca, no el plano. No se abrevian ni se dan por sobreentendidas:

```text
NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots,
NO whip pans, NO speed ramps, NO lens flares as decoration,
NO cheap CGI holograms, NO floating UI, NO glowing AI particles,
NO neon, NO teal-and-orange grade, NO oversaturated commercial colors,
NO corporate tech aesthetic, NO smiling stock actors, NO golden retriever,
NO barking dog, NO aggressive dog, NO tight leash, NO choke or prong collar,
NO slow-motion joy, NO product logos, NO on-screen text, NO watermark
```

---

## P01 · La calle a las 07:04

**Máster:** 00:00 — 00:07 · **Duración de generación:** 8 s · **Función:** encuadre canónico de la película

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Una mujer y su perro mestizo salen de un portal y **se detienen en seco** en la acera. Ella no avanza: está midiendo algo que el espectador todavía no ve. A más de 70 metros, al fondo a la derecha del encuadre y completamente desenfocada, otra silueta de una persona con otro perro viene hacia ellos por la acera de enfrente. La tensión no está en el fondo; está en que ella se ha parado. El reconocimiento que buscamos es doméstico y exacto: cualquiera que haya paseado un perro difícil ha hecho esa pausa en el umbral de su propio portal.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
ARRI ALEXA 65, anamórfico limpio, emulación de grano Kodak 5219 forzada un paso. Amanecer de invierno con bruma baja: una única fuente suave y direccional, sin relleno. Claroscuro sobrio y volumétrico — la bruma da cuerpo a la luz sin convertirla en haz de discoteca. El punto de negro se asienta muy bajo conservando detalle en las sombras; asfalto, ladrillo y pelaje leen como texturas, no como manchas. Paleta desaturada de grises fríos y marrones apagados; **el único color saturado permitido en cuadro es el rojo del portal metálico** (`#ef4444` como referencia, envejecido, nunca plano).

**3 · DINÁMICA DE CÁMARA**
Plano general **completamente fijo**, en trípode, a la altura de la espalda. Cero movimiento. La única evolución del plano es el foco: un *rack focus* mínimo y lentísimo que no llega a resolver la silueta del fondo — permanece deliberadamente irresuelta. La quietud absoluta de este plano es lo que hace legible el movimiento de P04.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Calle residencial española real, en pendiente muy suave. Portal de vidrio y metal envejecido, no arquitectura de catálogo. Acera mojada de rocío, coches aparcados cubiertos de escarcha, contenedores, una farola aún encendida. Cero decorado publicitario: ni escaparates iluminados, ni gente de fondo sonriendo. El aire se ve — vaho de las dos respiraciones. La ciudad está despierta pero vacía.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Fotorrealista, texturas 8k, renderizado natural de piel y pelo, fotografía de autor, profundidad atmosférica, movimiento de animal anatómicamente correcto, cero deformación del sujeto entre fotogramas. Más el bloque común de exclusiones (**R6**).

**CADENA PARA EL MOTOR**
```text
Locked-off wide cinematic shot on ARRI ALEXA 65 with clean anamorphic lenses,
35mm Kodak 5219 film grain pushed one stop. A quiet European residential street
on a gently sloping hill at 07:04 on a winter dawn, low ground fog, wet asphalt,
frost on parked cars, one streetlamp still lit. An early-forties woman,
shoulder-length dark brown hair loosely tied back, pale skin, no makeup,
charcoal wool coat over a grey sweater, black gloves, tired attentive face,
steps out of an aged glass-and-metal doorway with a medium-sized mixed-breed dog,
roughly 20 kg, short brindle and white coat with an irregular white patch on the
chest, upright expressive ears, plain flat black biothane collar. They stop dead
on the pavement. She does not move forward. Far in the background, over a hundred
metres away and completely out of focus, an unrecognisable silhouette walks
another dog across the street. Visible breath from both woman and dog in the cold
air. Naturalistic low-key single-source dawn light diffused by fog, masterclass
chiaroscuro, deep charcoal blacks retaining shadow detail, desaturated cold greys
and muted browns, the only saturated colour is the weathered red of the doorway
frame. Absolutely static tripod camera, no movement whatsoever, chest height,
extremely slow subtle rack focus that never resolves the distant silhouette.
Photorealistic, 8k textures, natural skin and fur rendering, award-winning
cinematography, atmospheric depth, anatomically correct animal motion.
NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots,
NO whip pans, NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms,
NO floating UI, NO glowing AI particles, NO neon, NO teal-and-orange grade,
NO oversaturated commercial colors, NO corporate tech aesthetic, NO smiling stock
actors, NO golden retriever, NO barking dog, NO aggressive dog, NO tight leash,
NO choke or prong collar, NO slow-motion joy, NO product logos, NO on-screen text,
NO watermark.
```
Locked-off wide cinematic shot from behind on ARRI ALEXA 65 with clean anamorphic lenses, 35mm Kodak 5219 film grain pushed one stop. A quiet European residential street on a gently sloping hill at 07:04 on a winter dawn, low ground fog, wet asphalt, frost on parked cars, one streetlamp still lit. 

The camera is positioned behind an early-forties woman with shoulder-length dark brown hair loosely tied back, wearing a charcoal wool coat. She and her medium-sized mixed-breed dog (roughly 20 kg, short brindle and white coat, upright expressive ears, plain flat black biothane collar) have just stepped out of an aged glass-and-metal doorway and stopped dead on the pavement. We see her from behind, remaining completely still, assessing the street ahead. 

Far in the background, over 70 meters away at the far right of the frame and completely out of focus, an unrecognizable silhouette of a person walking another dog is moving towards them along the opposite pavement. Visible breath from both woman and dog in the cold air. Naturalistic low-key single-source dawn light diffused by fog, masterclass chiaroscuro, deep charcoal blacks retaining shadow detail, desaturated cold greys and muted browns, the only saturated colour is the weathered red of the doorway frame. 

Absolutely static tripod camera, no movement whatsoever, chest height, composition focused on the tension of her sudden halt. Photorealistic, 8k textures, natural fur rendering, award-winning cinematography, atmospheric depth, anatomically correct animal motion. 

NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots, NO whip pans, NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms, NO floating UI, NO glowing AI particles, NO neon, NO teal-and-orange grade, NO oversaturated commercial colors, NO corporate tech aesthetic, NO smiling stock actors, NO golden retriever, NO barking dog, NO aggressive dog, NO tight leash, NO choke or prong collar, NO slow-motion joy, NO product logos, NO on-screen text, NO watermark.

---

## P02 · El bloqueo

**Máster:** 00:07 — 00:09 · **Duración de generación:** 5 s · **Función:** la reactividad contada sin reactividad

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Primer plano corto del perro, de perfil. Las orejas rotan hacia delante. El cuerpo se congela por completo. **Y deja de respirar durante un segundo entero.** No hay ladrido, ni gruñido, ni enseñar dientes: solo una interrupción del vaho que sale del hocico. Ese corte de la respiración es todo el plano y es lo que un dueño de perro reactivo reconoce al instante, porque es la señal que aprende a temer antes de que ocurra cualquier otra cosa.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Misma cámara y grano. Óptica larga, profundidad de campo muy corta: el ojo y la oreja en foco, el hocico ya cediendo. La luz de amanecer entra lateral y modela el pelo corto de la mejilla; el resto del cuerpo cae a penumbra. Renderizado de pelaje al detalle de pelo individual en la zona iluminada. Fondo reducido a un lavado gris-azulado sin información.

**3 · DINÁMICA DE CÁMARA**
Fijo, o un *push-in* de dos o tres centímetros a lo largo de los cinco segundos — al límite de lo perceptible. Nada más. La cámara observa a un animal; no lo persigue.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Aire frío visible. Cero atrezo. El plano contiene un animal, luz y temperatura. El perro debe leerse tranquilo y atento, no amenazante: el lenguaje corporal es de **orientación**, no de amenaza — sin labio levantado, sin pelo erizado, sin blanco del ojo.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Pelaje fotorrealista con pelo individual, movimiento ocular natural, anatomía canina correcta, sin morphing de la cara entre fotogramas. Más **R6**, con énfasis: **ningún signo de agresión o miedo.**

**CADENA PARA EL MOTOR**
```text
Tight cinematic close-up on ARRI ALEXA 65, long anamorphic lens, very shallow
depth of field, 35mm Kodak 5219 grain. Profile of a medium-sized mixed-breed dog,
short brindle and white coat, upright expressive ears, dark eyes, plain flat black
biothane collar. The ears rotate forward and the whole body goes completely still.
The visible breath vapour coming from its nose stops for one full second, then
resumes. Calm alert orientation, relaxed mouth, no teeth, no raised lip, no raised
hackles, no whale eye. Cold winter dawn air, side light from a low sun diffused by
fog sculpting the individual hairs on the cheek, the rest of the body falling into
deep shadow, background reduced to a featureless cold grey-blue wash. Camera locked
off or with an almost imperceptible two-centimetre push-in across five seconds,
nothing more. Photorealistic 8k fur with individual hair detail, natural eye
movement, anatomically correct canine structure, no facial morphing between frames.
NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots,
NO whip pans, NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms,
NO floating UI, NO glowing AI particles, NO neon, NO teal-and-orange grade,
NO oversaturated commercial colors, NO corporate tech aesthetic, NO smiling stock
actors, NO golden retriever, NO barking dog, NO aggressive dog, NO tight leash,
NO choke or prong collar, NO slow-motion joy, NO product logos, NO on-screen text,
NO watermark.
```

---

## P03 · La mano

**Máster:** 00:09 — 00:11 · **Duración de generación:** 5 s · **Función:** la tensión vive en la persona, no en el animal

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Macro de una mano enguantada sobre una correa de biothane negra. Los nudillos se marcan bajo el guante. **La correa no se tensa: lo que se cierra es el puño.** Esa distinción lo es todo — un tirón sería violencia sobre el animal; un puño que se cierra es miedo humano contenido. Al final del plano, casi imperceptiblemente, la mano se relaja.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Macro anamórfico, plano focal muy fino sobre los nudillos. Textura: cuero agrietado del guante, grano mate del biothane, hebra del puño del jersey asomando. Luz fría de amanecer desde arriba y a un lado; sombra profunda en la palma. Sin brillos especulares de estudio.

**3 · DINÁMICA DE CÁMARA**
Fijo absoluto. La única evolución es el micro-movimiento de la propia mano.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Correa negra mate, sin herrajes de marca, sin colores. Guante de cuero gastado, no técnico. Fondo: la manga del abrigo y aire desenfocado. Nada más entra en cuadro.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Anatomía de la mano correcta — cinco dedos, articulaciones creíbles, sin dedos extra ni deformación en el agarre; es el fallo más frecuente del plano. Piel fotorrealista. Más **R6**.

**CADENA PARA EL MOTOR**
```text
Extreme macro cinematic shot on ARRI ALEXA 65, anamorphic macro lens, razor-thin
focal plane, 35mm Kodak 5219 grain. A gloved adult hand gripping a matte black
biothane dog leash. The knuckles press up under worn leather as the fist tightens
around the leash, but the leash itself never goes taut. At the very end of the
shot the hand almost imperceptibly relaxes. Cracked leather glove texture, matte
biothane grain, a thread of grey sweater cuff showing at the wrist. Cold overhead
side dawn light, deep shadow in the palm, no studio specular highlights.
Completely locked-off camera, the only motion is the micro-movement of the hand
itself. Background is out-of-focus coat sleeve and cold air, nothing else in frame.
Anatomically perfect human hand with five fingers and believable joints,
photorealistic skin texture, no extra fingers, no deformation during the grip.
NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots,
NO whip pans, NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms,
NO floating UI, NO glowing AI particles, NO neon, NO teal-and-orange grade,
NO oversaturated commercial colors, NO corporate tech aesthetic, NO smiling stock
actors, NO golden retriever, NO barking dog, NO aggressive dog, NO tight leash,
NO choke or prong collar, NO slow-motion joy, NO product logos, NO on-screen text,
NO watermark.
```

---

## P04 · Los dos pasos atrás

**Máster:** 00:11 — 00:17 · **Duración de generación:** 8 s · **Función:** el plano de la película

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Ella mira al perro. Luego a la distancia. Y **da un paso hacia atrás. Y otro.** No tira de la correa. No dice nada. No mira el móvil. El perro la sigue sin resistencia y la correa, por primera vez, cuelga floja. La mancha desenfocada del fondo se aleja y el encuadre se abre. Es un retroceso, y hay que dirigirlo como una decisión: la cadencia es la de alguien que ejecuta un procedimiento, no la de alguien que huye.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Cámara baja, casi a la altura de los ojos del perro, lo que dignifica el gesto en lugar de empequeñecerlo. Misma bruma, misma fuente única de amanecer. Al abrirse el encuadre entra más aire y la profundidad atmosférica crece: la distancia se convierte en el sujeto visual del plano. Negros profundos, sin brillos.

**3 · DINÁMICA DE CÁMARA**
**Dolly de retroceso a la velocidad exacta de ella**, sobre raíles, absolutamente uniforme. La cámara se mueve porque ella se mueve; no interpreta. Sin balanceo, sin corrección de encuadre a media toma, sin aceleración. Si el movimiento se nota como movimiento de cámara, el plano ha fallado.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
La misma acera de P01, ahora vista a ras. Asfalto húmedo con reflejo tenue del cielo. Bruma que se espesa hacia el fondo. La segunda pisada debe caer **medio segundo más tarde** de lo que el espectador espera: esa vacilación es la interpretación entera.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Marcha humana hacia atrás natural y estable, mirada del perro coherente, correa con física creíble y siempre floja, sin patinaje de pies sobre el suelo. Más **R6**.

**CADENA PARA EL MOTOR**
```text
Low-angle cinematic tracking shot on ARRI ALEXA 65, clean anamorphic lens,
35mm Kodak 5219 grain, camera at dog eye height. An early-forties woman,
shoulder-length dark brown hair loosely tied back, charcoal wool coat over a grey
sweater, black gloves, looks down at her medium-sized mixed-breed dog with short
brindle and white coat and upright ears, then looks off into the distance, then
takes one deliberate step backwards, pauses, and takes a second step backwards.
She never pulls the leash. The dog follows her calmly without resistance and the
matte black leash hangs visibly slack. The out-of-focus silhouette far in the
background recedes further as the frame opens up. Winter dawn, low ground fog
thickening toward the background, wet asphalt faintly reflecting the sky, visible
breath. Naturalistic single-source diffused dawn light, deep charcoal blacks with
shadow detail, desaturated cold palette, growing atmospheric depth. Perfectly
smooth dolly pulling back on rails at exactly her walking speed, absolutely
uniform, no handheld sway, no reframing, no acceleration. Photorealistic 8k
textures, natural fur and skin rendering, stable natural backwards human gait,
believable leash physics always slack, no foot sliding, award-winning
cinematography.
NO hype, NO frenetic cutting, NO fast camera movement, NO drone or FPV shots,
NO whip pans, NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms,
NO floating UI, NO glowing AI particles, NO neon, NO teal-and-orange grade,
NO oversaturated commercial colors, NO corporate tech aesthetic, NO smiling stock
actors, NO golden retriever, NO barking dog, NO aggressive dog, NO tight leash,
NO choke or prong collar, NO slow-motion joy, NO product logos, NO on-screen text,
NO watermark.
```

---

## P05 · Placa de móvil

**Máster:** 00:17 — 00:25 · **Duración de generación:** 8 s · **Función:** placa para composición de UI — **la pantalla se genera apagada**

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Inserto sobre el hombro: el móvil apoyado en el antebrazo, sostenido con una mano, mientras el pulgar recorre la pantalla de arriba abajo y luego pulsa una vez. El gesto es de **rellenar un registro**, no de consumir contenido: pausas cortas entre campos, sin arrastres largos, sin scroll ansioso. La UI entra después en post; lo que genera el motor es la mano, la luz y el gesto.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Macro anamórfico. **La pantalla del teléfono está apagada y en negro puro**, actuando como espejo oscuro de la luz gris del amanecer. Sin brillo de pantalla iluminando el rostro — esa luz se añade en post junto con la interfaz. Foco sobre el pulgar y el borde del dispositivo. Grano presente.

**3 · DINÁMICA DE CÁMARA**
Fijo, sujeto sobre soporte. El plano no se mueve en absoluto: cualquier deriva complica el *tracking* de la composición posterior.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Teléfono negro mate genérico **sin logotipo ni marca reconocible**, sin funda de color, pantalla limpia sin arañazos. Manga de abrigo de lana carbón. Fondo: acera desenfocada. Luz plana de amanecer nublado — sin sol directo, para que la iluminación de pantalla añadida en post sea creíble.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Pantalla uniformemente negra sin ningún contenido, texto, icono ni resplandor. Anatomía de mano correcta. Sin logotipo de fabricante. Sin reflejos móviles que impidan la composición. Más **R6**, con énfasis absoluto en **NO on-screen text** y **NO glowing screen**.

**CADENA PARA EL MOTOR**
```text
Locked-off macro insert shot on ARRI ALEXA 65, anamorphic macro lens,
35mm Kodak 5219 grain, camera rigidly mounted with zero drift. Over-the-shoulder
view of a matte black generic smartphone with no visible brand or logo, resting on
a forearm in a charcoal wool coat sleeve, held in one gloved-off hand. THE PHONE
SCREEN IS COMPLETELY OFF, pure black, acting as a dark mirror reflecting the flat
grey dawn sky. No screen glow, no light from the phone on the face or hand.
The thumb moves down the dark screen in short deliberate pauses, as if filling in
a form field by field, then presses once and stops. Flat overcast winter dawn
light, no direct sun. Focus on the thumb and the edge of the device, out-of-focus
wet pavement in the background. Photorealistic 8k skin texture, anatomically
perfect hand with five fingers, clean unscratched screen surface.
NO on-screen text, NO screen glow, NO icons, NO user interface, NO app, NO logos,
NO brand marks, NO reflections that obscure the screen surface, NO hype,
NO frenetic cutting, NO fast camera movement, NO drone or FPV shots, NO whip pans,
NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms, NO floating
UI, NO glowing AI particles, NO neon, NO teal-and-orange grade, NO oversaturated
commercial colors, NO corporate tech aesthetic, NO smiling stock actors,
NO golden retriever, NO barking dog, NO slow-motion joy, NO watermark.
```

> **Composición en post.** Sobre esta placa se integra la UI descrita en [02 · §00:17](02-guion-spot-60s.md): tarjeta `REPORTE DE SESIÓN` y su sustitución por `DECISIÓN · REDUCIR UNA DIMENSIÓN` con acento ámbar `#f59e0b`. Rótulo `DATOS DE DEMOSTRACIÓN` arriba a la derecha. Añadir en composición el rebote de luz de pantalla sobre los dedos, o el plano delatará el truco.

---

## P06 · Ella

**Máster:** 00:25 — 00:31 · **Duración de generación:** 8 s · **Función:** soporte de la voz en off 1

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Rostro a tres cuartos. **No sonríe. No llora. Suelta el aire.** La indicación de dirección es una sola: *no interpretes alivio; interpreta que acabas de entender algo*. Un parpadeo lento, la mandíbula que se destensa, la exhalación visible en el frío. Nada más ocurre en seis segundos, y esa es exactamente la apuesta de atención de la película.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Óptica media-larga, profundidad corta. Luz de amanecer desde un lado modelando media cara; la otra mitad cae a penumbra con detalle. Claroscuro de retrato clásico, sin relleno de belleza. Piel real: poros, frío en la nariz y los pómulos, sin retoque. Fondo desenfocado a un lavado gris.

**3 · DINÁMICA DE CÁMARA**
*Push-in* muy lento y perfectamente uniforme sobre seis segundos, apenas unos centímetros. La cámara se acerca porque el pensamiento se acerca. Sin ajuste de encuadre, sin balanceo.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Sin atrezo. Cuello de abrigo de lana, mechón suelto, vaho. La calle existe solo como textura fuera de foco.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Piel fotorrealista sin suavizado, micro-expresión estable sin deriva facial entre fotogramas, ojos que no cambian de color ni de forma, parpadeo natural. Más **R6**, con énfasis: **no sonreír en ningún fotograma.**

**CADENA PARA EL MOTOR**
```text
Slow push-in cinematic portrait on ARRI ALEXA 65, medium-long anamorphic lens,
shallow depth of field, 35mm Kodak 5219 grain. Three-quarter view of an
early-forties woman, shoulder-length dark brown hair loosely tied back, pale skin
reddened by cold at the nose and cheekbones, no makeup, charcoal wool coat collar
turned up, a loose strand of hair across her face. She does not smile and does not
cry. She blinks slowly, her jaw unclenches, and she releases a long visible breath
into the cold air. The expression is quiet comprehension, not relief. Winter dawn
side light sculpting one half of the face, the other half falling into deep shadow
that still holds detail, classical portrait chiaroscuro, no beauty fill light, no
skin smoothing. Background dissolved into an out-of-focus grey wash. Extremely slow
perfectly uniform push-in of only a few centimetres over the full shot, no
reframing, no sway. Photorealistic 8k skin with visible pores, stable
micro-expression with zero facial drift between frames, consistent eye colour and
shape, natural blinking.
NO smiling at any frame, NO tears, NO hype, NO frenetic cutting, NO fast camera
movement, NO drone or FPV shots, NO whip pans, NO speed ramps, NO lens flares as
decoration, NO cheap CGI holograms, NO floating UI, NO glowing AI particles,
NO neon, NO teal-and-orange grade, NO oversaturated commercial colors, NO corporate
tech aesthetic, NO smiling stock actors, NO slow-motion joy, NO product logos,
NO on-screen text, NO watermark.
```

---

## P07 · El despacho

**Máster:** 00:31 — 00:37 · **Duración de generación:** 8 s · **Función:** el otro lado del mismo caso

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Una profesional de conducta, cuarenta y tantos, abre un portátil a las 08:12 y **no abre mensajes: abre un caso.** Lee unos segundos. Después escribe una nota corta, con dos dedos, sin prisa. El gesto que buscamos es el de alguien que documenta una decisión que va a tener que defender, no el de alguien que responde un chat. Sus manos son manos de trabajo.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Interior en penumbra natural. **Dos fuentes y ninguna más:** una ventana lateral fría a media mañana y el propio panel del portátil, que le levanta la mitad inferior del rostro. Claroscuro denso, negros profundos con detalle en las estanterías. Paleta de maderas apagadas, gris y azul marino. Grano presente.

**3 · DINÁMICA DE CÁMARA**
*Dolly* lateral lentísimo a la izquierda, de unos pocos centímetros, o plano fijo si el motor introduce deriva. Movimiento observacional: la cámara está en la habitación, no opinando sobre ella.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Despacho pequeño y **real**: libros usados con lomos rozados, carpetas, una taza de café sin tocar, una silla desparejada, un cable visible. **Sin bata blanca, sin plató clínico, sin pared de diplomas, sin planta de decoración.** El producto no diagnostica y el encuadre no debe sugerir consulta médica. Portátil mate genérico, sin logotipo.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Anatomía de manos correcta al teclear, tipografía ilegible en el portátil por ángulo y foco, iluminación de pantalla creíble sobre el rostro. Más **R6**, y además: **NO lab coat, NO clinic, NO medical setting.**

**CADENA PARA EL MOTOR**
```text
Atmospheric interior medium shot on ARRI ALEXA 65, clean anamorphic lens,
35mm Kodak 5219 grain. A woman in her mid-forties, short greying hair, dark navy
sweater, reading glasses pushed up on her head, working hands, sits at a small
cluttered desk in a real cramped home office at 08:12 in the morning. She opens a
matte generic laptop with no visible brand, reads for a few seconds, then types a
short note with two fingers, unhurried and deliberate. Only two light sources: a
cold side window and the laptop panel itself lifting the lower half of her face.
Dense chiaroscuro, deep blacks retaining detail in the bookshelves behind her,
muted wood, grey and navy palette. Production design of worn used books with
scuffed spines, paper folders, an untouched cup of black coffee, a mismatched
chair, a visible cable. Extremely slow lateral dolly left of a few centimetres, or
fully locked off. Photorealistic 8k textures, natural skin rendering, anatomically
correct hands while typing, believable screen light on the face, laptop screen
content illegible due to angle and focus.
NO lab coat, NO clinic, NO medical setting, NO wall of diplomas, NO decorative
plant, NO tidy showroom desk, NO hype, NO frenetic cutting, NO fast camera
movement, NO drone or FPV shots, NO whip pans, NO speed ramps, NO lens flares as
decoration, NO cheap CGI holograms, NO floating UI, NO glowing AI particles,
NO neon, NO teal-and-orange grade, NO oversaturated commercial colors, NO corporate
tech aesthetic, NO smiling stock actors, NO product logos, NO on-screen text,
NO watermark.
```

---

## P08 · Placa de portátil

**Máster:** 00:37 — 00:41 · **Duración de generación:** 6 s · **Función:** placa para composición de UI — **la pantalla se genera apagada**

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
Inserto cerrado sobre la pantalla del portátil y las manos que teclean. Aquí es donde la película demuestra su tesis sin decirla: lo que llega de casa no es «ha ido bien», es un registro con hora, resultado, señales y decisión. La UI se compone en post. El motor genera manos, madera, luz y el marco del dispositivo.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Macro anamórfico en ángulo bajo respecto al panel. **Pantalla apagada, negro puro**, reflejando débilmente la ventana lateral. Foco sobre el borde del teclado y las yemas. Sin brillo de pantalla — se añade en post con la interfaz.

**3 · DINÁMICA DE CÁMARA**
Fijo absoluto sobre soporte rígido. Cero deriva: es requisito de composición, no preferencia estética.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
Portátil negro mate **sin logotipo ni forma de marca reconocible**. Mesa de madera gastada, un cuaderno abierto con escritura a mano fuera de foco, la taza al borde del cuadro. Luz lateral fría.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Pantalla uniformemente negra, sin texto, iconos, ventanas ni resplandor. Sin logotipo de fabricante. Anatomía de manos correcta. Más **R6**, con énfasis en **NO on-screen text** y **NO glowing screen**.

**CADENA PARA EL MOTOR**
```text
Locked-off macro insert on ARRI ALEXA 65, anamorphic macro lens, 35mm Kodak 5219
grain, camera rigidly mounted with absolutely zero drift. Low angle across the
open panel of a matte black laptop with no visible brand or logo shape. THE LAPTOP
SCREEN IS COMPLETELY OFF, pure black, faintly mirroring a cold side window. No
screen glow and no light from the screen on the hands. Two adult hands with short
unpolished nails type a few slow deliberate keystrokes and then rest. Worn wooden
desk surface, an open paper notebook with out-of-focus handwriting, the edge of a
coffee cup at the frame border. Cold directional window light from the left, deep
shadows. Photorealistic 8k textures, anatomically correct hands with five fingers,
realistic keyboard interaction, natural skin.
NO on-screen text, NO screen glow, NO icons, NO windows, NO user interface,
NO logos, NO brand marks, NO hype, NO frenetic cutting, NO fast camera movement,
NO drone or FPV shots, NO whip pans, NO speed ramps, NO lens flares as decoration,
NO cheap CGI holograms, NO floating UI, NO glowing AI particles, NO neon,
NO teal-and-orange grade, NO oversaturated commercial colors, NO corporate tech
aesthetic, NO watermark.
```

> **Composición en post.** Sobre esta placa se integra la ficha `CASO · BANGO`, la línea de atención en ámbar `#f59e0b` y el rastro de auditoría `editado por A. Ruiz · 08:12`, según [02 · §00:31](02-guion-spot-60s.md). Rótulo `DATOS DE DEMOSTRACIÓN`. Añadir rebote de pantalla sobre manos y mesa.

---

## P09 · Tres mañanas

**Máster:** 00:41 — 00:50 · **Duración de generación:** 3 clips × 6 s · **Función:** el dispositivo formal de la película

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
El mismo encuadre exacto de P01, tres veces, en tres días distintos. Solo cambian la luz y el clima. En la primera, lluvia fina; ella y el perro esperan. En la segunda, cielo cubierto; ninguno de los dos se mueve. En la tercera, sol bajo sin bruma: el perro mira la silueta lejana y **gira la cabeza hacia ella por su cuenta**, sin que ella haya dicho ni hecho nada. Ese giro voluntario de cabeza es el único acontecimiento del acto tercero. La repetición del encuadre es lo que convierte tres planos bonitos en una demostración de método.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Idéntica óptica, altura y eje que P01 — no aproximados: idénticos. La única variable de fotografía es la meteorología:
- **Clip A:** lluvia fina, luz plana y difusa, asfalto brillante, paleta gris-azulada, contraste bajo.
- **Clip B:** cielo cubierto denso, sin sombras, luz muerta y uniforme, el plano más apagado de los tres.
- **Clip C:** sol bajo y limpio sin bruma, sombras largas por la izquierda, primer momento cálido de la película — cálido de temperatura de color, no de saturación.

**3 · DINÁMICA DE CÁMARA**
Fijo absoluto en los tres. Cero movimiento, cero corrección. Cualquier deriva entre clips destruye el efecto.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
El mismo tramo de acera, el mismo portal, los mismos coches en las mismas plazas. Continuidad de vestuario con una única variación deliberada por clip —bufanda en A, sin bufanda en C— que confirme al espectador que son días distintos y no tomas distintas.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Identidad de sujeto y perro estable entre los tres clips, encuadre idéntico, geometría del fondo idéntica. Más **R6**, y además: **NO time-lapse, NO dissolve, NO seasonal change, NO montage effect.** Son tres días, no una transición.

**CADENA PARA EL MOTOR** *(base común; sustituir el bloque `[VARIANTE]` en cada clip)*
```text
Locked-off wide cinematic shot on ARRI ALEXA 65, clean anamorphic lens, 35mm Kodak
5219 grain, tripod at chest height, absolutely no camera movement. The exact same
European residential street on a gently sloping hill, the same aged glass-and-metal
doorway, the same parked cars in the same spaces. An early-forties woman,
shoulder-length dark brown hair loosely tied back, charcoal wool coat over a grey
sweater, stands on the pavement with her medium-sized mixed-breed dog, short
brindle and white coat with an irregular white chest patch, upright expressive
ears, plain flat black biothane collar, leash hanging slack. Far in the background,
over a hundred metres away and completely out of focus, an unrecognisable
silhouette walks another dog. [VARIANTE] Photorealistic, 8k textures, natural skin
and fur rendering, award-winning cinematography, atmospheric depth, stable subject
identity, anatomically correct animal motion.
NO time-lapse, NO dissolve, NO seasonal change, NO montage effect, NO hype,
NO frenetic cutting, NO fast camera movement, NO drone or FPV shots, NO whip pans,
NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms, NO floating
UI, NO glowing AI particles, NO neon, NO teal-and-orange grade, NO oversaturated
commercial colors, NO corporate tech aesthetic, NO smiling stock actors, NO golden
retriever, NO barking dog, NO aggressive dog, NO tight leash, NO choke or prong
collar, NO slow-motion joy, NO product logos, NO on-screen text, NO watermark.
```

**Bloques `[VARIANTE]`:**

```text
CLIP A — Light drizzle, flat diffused overcast light, glossy wet asphalt, cold
grey-blue palette, low contrast, she wears a dark scarf. Both woman and dog simply
wait, still, looking down the street.

CLIP B — Dense flat overcast, no shadows at all, dead uniform light, the most
muted and desaturated of the three. Neither of them moves. She wears the same dark
scarf.

CLIP C — Low clean winter sun, no fog, long shadows raking in from the left, the
first warm colour temperature of the film though still desaturated. No scarf.
The dog looks toward the distant silhouette, then voluntarily turns its head back
to the woman on its own, unprompted, while she stays completely still and silent.
```

---

## P10 · La calle vacía

**Máster:** 00:50 — 00:56 · **Duración de generación:** 10 s · **Función:** el remate; los metros que cedieron

**1 · GANCHO VISUAL Y ACCIÓN CENTRAL**
El cuarto uso del mismo encuadre. Ella y el perro caminan y **salen de cuadro por la izquierda**, sin prisa, con la correa floja. La cámara no los sigue. Se queda sobre la calle vacía durante cuatro segundos completos. En una pausa publicitaria de Super Bowl, cuatro segundos de calle vacía son una eternidad, y ese es el punto: el spot termina mirando el terreno que se cedió a propósito.

**2 · ESTÉTICA Y DIRECCIÓN DE FOTOGRAFÍA**
Misma óptica y encuadre que P01 y P09. Sol bajo y limpio de la mañana del clip C, sombras largas, la sombra de los dos abandonando el cuadro después que ellos. Los negros se mantienen profundos incluso con la luz más alta de la película. Grano visible en el cielo.

**3 · DINÁMICA DE CÁMARA**
Fijo absoluto. **La cámara no panea, no sigue, no reencuadra.** Ésta es la instrucción más importante del plano y la que más probablemente ignore un motor generativo: si el clip la sigue, se regenera.

**4 · DISEÑO DE PRODUCCIÓN Y ATMÓSFERA**
La acera exacta, vacía. Vapor de una rejilla lejana, una hoja moviéndose, el zumbido de una ciudad que empieza. La calle no está muerta: está disponible.

**5 · CONTROLES DE CALIDAD Y EXCLUSIONES**
Los sujetos salen limpiamente de cuadro y no reaparecen. Nadie más entra en el plano. La geometría del fondo permanece estable. Más **R6**, y además: **NO camera pan, NO follow, NO reframe, NO new characters entering frame.**

**CADENA PARA EL MOTOR**
```text
Locked-off wide cinematic shot on ARRI ALEXA 65, clean anamorphic lens, 35mm Kodak
5219 grain, tripod at chest height, absolutely no camera movement of any kind.
The same European residential street on a gently sloping hill, same aged
glass-and-metal doorway, same parked cars. Low clean winter morning sun, long
shadows raking in from the left. An early-forties woman in a charcoal wool coat
walks unhurried with her medium-sized brindle and white mixed-breed dog on a
visibly slack matte black leash, and they exit the frame to the left, their long
shadows leaving the frame after them. The camera does not follow them. The shot
then holds on the completely empty street for four full seconds. Faint steam from
a distant vent, one leaf moving, a city beginning to wake. Deep charcoal blacks
retaining detail even at the brightest light level of the film, visible grain in
the sky. Photorealistic, 8k textures, award-winning cinematography, atmospheric
depth, stable background geometry.
NO camera pan, NO follow, NO reframe, NO new characters entering frame, NO hype,
NO frenetic cutting, NO fast camera movement, NO drone or FPV shots, NO whip pans,
NO speed ramps, NO lens flares as decoration, NO cheap CGI holograms, NO floating
UI, NO glowing AI particles, NO neon, NO teal-and-orange grade, NO oversaturated
commercial colors, NO corporate tech aesthetic, NO smiling stock actors, NO golden
retriever, NO barking dog, NO slow-motion joy, NO product logos, NO on-screen text,
NO watermark.
```

---

## No generativo

Estas piezas **no se piden a ningún motor**. Se construyen en diseño y composición, con los tipos y tokens del design system:

| Elemento | Máster | Producción |
|---|---|---|
| Rótulo `07:04 · 8 m → 12 m` | 00:11 — 00:17 | Diseño · JetBrains Mono 300 |
| Toda la UI de móvil | 00:17 — 00:25 | Render de UI + composición sobre P05 |
| Toda la UI de portátil | 00:31 — 00:41 | Render de UI + composición sobre P08 |
| `Criterio cumplido — por encima del 80 %` | 00:47 | Composición sobre P09 clip C |
| Cartones narrativos A y B | 00:56 — 00:58 | Diseño · Space Grotesk, sentence case |
| Cartón de marca | 00:58 — 01:00 | Diseño · marca + descriptor |

---

## Orden de generación recomendado

1. **P01** primero, siempre. Es el encuadre canónico y la referencia de identidad de reparto de toda la pieza.
2. **P09 clips A/B/C** y **P10**, usando P01 como referencia de imagen. Si no se consigue un encuadre idéntico, se detiene la generación y se rueda: el dispositivo formal no admite aproximación.
3. **P04**, el plano de la película. Presupuestar más iteraciones aquí que en ningún otro: marcha hacia atrás, física de correa y velocidad de dolly rara vez salen a la primera.
4. **P02, P03, P06**, planos cerrados de un solo sujeto, los más fiables.
5. **P07**, interior.
6. **P05 y P08**, placas, al final, cuando los renders de UI ya estén aprobados y se conozca el ángulo exacto que necesita la composición.

**Criterio de parada por plano:** si tras ocho iteraciones el plano sigue fallando en identidad de sujeto, anatomía de mano o estabilidad de encuadre, pasa a rodaje. Los diez planos son rodables. La generación aquí es una herramienta de previsualización y de coste, no un fin.
