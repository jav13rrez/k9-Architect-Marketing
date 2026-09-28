# K9 Architect — 16 prompts de vídeo IA (15 s, formato final)

**Deriva de:** [`guiones-16-reels-shotlist-2026-09-28.md`](guiones-16-reels-shotlist-2026-09-28.md) (Mode D, narrativa y razón de cada plano ya fijadas ahí). Este documento es la salida **Mode F** de `cinematic-director`: prompts de generación de vídeo, no la explicación de por qué.

## Marco de trabajo (asunciones, una línea cada una)

- **Duración final por pieza: 15 s.** Estructura fija en 3 segmentos de 5 s cada uno: `[00:00–00:05]` desencadenante, `[00:05–00:10]` manifestación/clímax, `[00:10–00:15]` desenlace humano.
- **Forma de prompt: S4, multi-shot con timestamps**, texto a vídeo directo (sin keyframe previo). Es agnóstico de herramienta: sirve tal cual en un modelo con soporte multi-shot (Veo, Kling 2.5+, Sora-class, Hailuo 2.3); si tu herramienta solo genera clips cortos sueltos, cada `[mm:ss–mm:ss] Shot N` se parte en un prompt S2 independiente y se encadenan/extienden en montaje — dímelo y te los separo.
- **Idioma del prompt: inglés** (estándar de la mayoría de modelos), con la etiqueta en español al lado para que sigas el hilo narrativo.
- **Sin diálogo nativo del modelo.** El habla del tutor (`«¡Siéntate!»`, etc.) se trata como VO/doblaje añadido en posproducción, no como audio generado — más fiable en cualquier herramienta y evita la lotería de labios/voz de los modelos actuales.
- **El end card de marca (logo, CTA, `Aplicación web · 7 días sin tarjeta`) NO se genera por IA.** Se superpone en montaje sobre el último segundo del clip 3, usando la plantilla ya fijada en el guion madre. Generar una interfaz o un logo por IA sería inventar producto — eso sigue siendo una línea dura, no de tono.
- **Contacto físico de riesgo (dentellada, mordida):** en todos los prompts la acción se corta justo antes del contacto y el segundo siguiente empieza ya en la reacción humana. Es más fiable para el modelo (los modelos actuales generan mal el contacto físico realista) y es, además, la misma decisión de bienestar que ya regía el guion madre.
- **Negativo estándar**, se añade a los 16 sin repetirlo cada vez: `no text overlay, no logos, no watermark, no extra people, no deformed hands, no deformed paws, no breed change, no lighting change between shots, no camera shake beyond specified movement`.

---

## V01 · Reactividad por frustración

**Continuidad:** Dog — medium-large mixed-breed dog, short tan coat, erect ears, natural bobtail wagging stiffly. Tutor — woman, early 30s, dark raincoat, hair tied back. Location — narrow European city sidewalk, overcast daylight, worn pavement, parked bikes in background.

```text
Overall: Handheld observational realism, slightly unsteady camera, natural overcast daylight, muted urban palette. Same woman in dark raincoat and same tan medium-large mixed-breed dog with erect ears throughout. Leash is a plain fabric leash, held short.

[00:00-00:05] Shot 1: Wide shot at street level, camera handheld but mostly still. Another dog and owner appear calmly 25 meters down the narrow sidewalk. The tan dog stops walking abruptly, body goes rigid, ears point forward, tail rises and vibrates. The woman's hand wraps the leash tighter around her fist in a quick reflex motion. No camera movement beyond a slow creep forward.

[00:05-00:10] Shot 2: Medium shot, handheld, camera shake increases with the action. The dog lunges forward against the leash, front paws leaving the ground, coughing once from the pressure on its neck. The woman plants her feet, leans back against the pull, mouth open as if shouting. Leash stays taut throughout, dog never breaks free.

[00:10-00:15] Shot 3: Static medium close shot, camera locked. The other dog and owner have already left the frame. The tan dog stands with tongue hanging out, panting hard, eyes unfocused, body sagging. The woman's shoulders drop, she exhales visibly, looking down at the dog. Shot ends held on her lowered, tired expression.

Negative: no bite contact, no dogs touching, no aggressive contact between the two dogs, no visible cars or pedestrians close to the action, no readable text or signage in frame.
```

---

## V02 · Reactividad por miedo ⚠️

**Continuidad:** Dog — medium mixed-breed dog, black-and-white coat, soft rounded ears. Tutor — man, 40s, short beard, dark puffer jacket. Stranger — person in bulky beige coat, face not emphasized. Location — same type of narrow city sidewalk, overcast, different corner with a blind turn.

```text
Overall: Handheld realism, cool overcast light, tense and quiet — no music implied, ambient street sound only. Same black-and-white medium dog and same man in dark puffer jacket throughout. Leash short and taut.

[00:00-00:05] Shot 1: Low, close handheld shot on the dog's face and front paws. The dog licks its nose quickly, lowers its center of gravity, ears flatten slightly, weight shifts backward as if trying to retreat. The leash stays visibly taut, preventing any backward movement. Camera holds close, minimal movement.

[00:05-00:10] Shot 2: Wide static shot. A person in a bulky beige coat turns a blind corner abruptly, walking normally, unaware of the dog. Camera does not move. Hold on the empty space between the dog and the stranger closing.

[00:10-00:15] Shot 3: Medium close shot on the man's face and upper body only, camera locked, no dog or stranger visible in frame. His expression shifts fast from calm to alarmed, he yanks his arm backward sharply and his mouth opens as if shouting. He then crouches slightly, one hand out defensively. End on his tense, apologetic expression.

Negative: no bite contact visible, no teeth visible on the dog, no stranger's face in close-up, no blood, no visible injury.
```

**Nota:** único guion del lote donde el CTA final del propio vídeo (fuera de este prompt, se añade en montaje) debe apuntar a derivación/profesional, no a alta.

---

## V03 · Ansiedad por separación — pánico vocal

**Continuidad:** Dog — medium golden-brown mixed-breed dog, floppy ears. Tutor — woman, late 20s, casual work clothes, canvas tote bag. Location — small apartment entryway, warm indoor lamp light, coat hooks and a shoe rack by the door.

```text
Overall: Warm, intimate indoor light from a single lamp, handheld but calm camera in the first half, then a static locked shot. Same golden-brown medium dog and same young woman throughout. Entryway with a wooden door, brass door handle, hooks with keys.

[00:00-00:05] Shot 1: Close handheld shot on a set of keys being lifted off a wall hook. Camera tilts down to reveal the dog already standing, pupils wide, panting though the room is not warm, pressed close against the woman's legs. She crouches briefly, cupping the dog's face gently. Camera holds mostly still with a small handheld drift.

[00:05-00:10] Shot 2: Static locked shot on the closed apartment door from inside, key turning audible off-screen, door closing. A beat of silence, then the dog's front paws jump against the door repeatedly, scratching at the wood near the handle. Camera does not move at all.

[00:10-00:15] Shot 3: Wide static shot down an empty hallway, door in the background, no person in frame. Faint continuous sound of the dog behind the door. Camera holds completely still for the full five seconds, no movement, emphasizing the empty space.

Negative: no visible damage to the door, no blood on paws, no other people in frame, no exterior street visible.
```

---

## V04 · Ansiedad por separación — destructividad

**Continuidad:** Dog — medium-large mixed-breed dog, dark brindle coat. Tutor — man, 30s, casual shirt. Location — apartment living room, wooden door frame, window with blinds, evening light through blinds.

```text
Overall: Naturalistic indoor light shifting from afternoon to evening across the sequence, mostly static camera. Same brindle medium-large dog only in shot 1; dog is absent from shots 2 and 3 by design. Same man in casual shirt in shot 3.

[00:00-00:05] Shot 1: Static wide shot of a living room, front door closing in the background, wall clock visible showing the time. Light shifts subtly warmer to indicate hours passing, implied through a slow, almost imperceptible dim of the lamp light rather than any character movement. No dog in later part of shot.

[00:05-00:10] Shot 2: Close static shot on a wooden door frame at floor level, un-damaged at the start. Over the five seconds, wood splinters appear gradually at the base of the frame as if freshly chewed, small shavings scattering — object animation only, no animal in frame at any point.

[00:10-00:15] Shot 3: Medium shot, key turning in a door lock (sound cue), door opens to reveal the same living room now with a slightly torn blind and scattered wood shavings on the floor. The man steps in, stops abruptly, one hand goes to his mouth. Camera holds static on his shocked, tired expression.

Negative: no dog visible with damaged objects, no dog with visible injury or blood, no dog chewing shown in progress, no bared teeth.
```

---

## V05 · Fobia acústica

**Continuidad:** Dog — senior small-medium mixed-breed dog, graying muzzle, short gray-brown coat. Tutor — woman, 50s, casual home clothes. Location — apartment window and hallway, then a small bathroom, night lighting.

```text
Overall: Naturalistic light, cool and dim, near-silent sound design apart from specified cues — no score. Same graying senior dog and same woman throughout. Time of day shifts from evening storm to deep night.

[00:00-00:05] Shot 1: Static wide shot through a window, dark clouds visible, a single distant flash of lightning with a delayed low thunder rumble. Camera holds completely still on the window and room interior, dog not yet visible.

[00:05-00:10] Shot 2: Handheld shot following low and close behind the dog's body at floor level as it moves quickly and erratically down a hallway, ears back, body trembling, trying to squeeze into a narrow gap beside a bathroom cabinet. Camera stays close and low throughout, unsteady but controlled.

[00:10-00:15] Shot 3: Static medium shot, cool bathroom light, the woman sitting on the floor with the trembling dog held gently against her, both still, dog's body faintly shaking. Timestamp graphic implied by scene stillness only, no camera movement for the full five seconds.

Negative: no exaggerated shaking (keep tremor subtle and physically plausible), no dog vocalizing distress sounds in a way that reads as painful, no visible self-injury.
```

---

## V06 · Protección de recursos con comida ⚠️

**Continuidad:** Dog — medium stocky mixed-breed dog, short brown coat. Tutor — man, 30s, home clothes, short sleeves. Location — living room with a dog bed on the floor near a rug, daytime soft light.

```text
Overall: Calm naturalistic light at the start, tension conveyed through stillness and framing rather than movement. Same brown stocky dog and same man throughout. High-value chew item is a generic pressed bone shape, no branding visible.

[00:00-00:05] Shot 1: Medium static shot, the dog lying calmly on its bed chewing a bone-shaped item. The man's feet and legs enter frame from the side, walking closer at a normal pace. Camera does not move.

[00:05-00:10] Shot 2: Close shot on the dog's eye and muzzle, body freezes completely, eye rolls sideways showing the white (whale eye), head lowers slightly over the item. Camera holds very still, minimal creep-in only.

[00:10-00:15] Shot 3: Medium close shot on the man's hand and forearm reaching toward the dog, stopping short — the hand pulls back sharply mid-motion as if startled, out of instinct. Cut is implied at the pull-back; the dog's mouth and the hand are never shown in contact. End on the man's hand withdrawn, his face concerned in the background, out of focus.

Negative: no visible teeth contact with the hand, no snapping motion shown completing, no blood, no close-up of bared teeth.
```

**Nota:** CTA final (montaje, fuera de este prompt) suavizado hacia «con un profesional delante», no alta directa.

---

## V07 · Protección de recursos sobre mobiliario/tutor ⚠️

**Continuidad:** Dog — medium mixed-breed dog, cream-colored coat. Tutor A (dueña principal) — woman, 40s. Tutor B (familiar) — man, 40s. Location — living room sofa, warm evening lamp light.

```text
Overall: Warm domestic evening light, calm start turning tense through stillness and proximity, not through fast cuts. Same cream-coated dog, same woman, same second man throughout.

[00:00-00:05] Shot 1: Medium wide static shot, the dog sleeping curled against the woman on the sofa. The man enters frame from the side, walking at a normal pace toward the sofa with the intention to sit. Camera does not move.

[00:05-00:10] Shot 2: Close shot on the dog's face, eyes snapping open, jaw tensing visibly, body completely still, not moving away. The man's hand enters frame reaching toward the dog's collar. Camera holds still, slight creep only.

[00:10-00:15] Shot 3: Medium shot on the woman's face and upper body only, her expression shifting to alarm, mouth opening as if shouting toward the dog, one arm gesturing protectively. The dog and the other man are only partially visible at the edge of frame, motion blurred and brief. End held on the woman's tense face.

Negative: no bite contact shown, no teeth in close-up, no physical contact between the man's hand and the dog's mouth.
```

**Nota:** CTA suavizado — informe/ajuste del profesional, no alta directa.

---

## V08 · Agresividad por dolor físico oculto ⚠️

**Continuidad:** Dog — senior medium mixed-breed dog, graying around the muzzle, stiff gait. Tutor — woman, 50s, casual home clothes, sleeves rolled up. Location — living room rug, gray daylight through a rain-streaked window.

```text
Overall: Cold gray daylight, quiet, contemplative pacing, minimal camera movement throughout. Same graying senior dog and same woman throughout. A folded towel is a consistent prop.

[00:00-00:05] Shot 1: Static wide shot, the dog resting on a rug after a walk, damp fur. The woman kneels beside it with a towel, beginning to dry its hind legs and hip area gently. Camera does not move.

[00:05-00:10] Shot 2: Close shot on the dog's ears and face, ears flattening slightly, breathing pausing for a beat as the towel touches the hip area. Camera holds still, very slight creep-in only.

[00:10-00:15] Shot 3: Medium shot on the woman's forearm and face together, her arm withdrawing sharply and her face shifting to a shocked, hurt expression as she looks at her own wrist — no wound is shown explicitly, just her reaction and her hand cradling her own arm. The dog, out of focus in the background, shifts away with head lowered. End on her shocked expression.

Negative: no visible bite mark or wound, no blood, no bared teeth in close-up, no explicit contact moment shown.
```

**Nota:** CTA final = derivación veterinaria explícita, no alta. Es el eje del vídeo, no una concesión.

---

## V09 · Ladrido de alarma ante visitas

**Continuidad:** Dog — medium-large mixed-breed dog, black coat, alert prick ears. Tutor — man, 30s, home clothes. Location — apartment entryway near the front door, calm afternoon light.

```text
Overall: Calm static light at the start, handheld energy rising with the action. Same black medium-large dog and same man throughout. Front door is plain wood with a peephole.

[00:00-00:05] Shot 1: Static wide shot, quiet living room, the dog asleep. A doorbell sound cue plays. The dog's body snaps upright instantly, fur along the spine visibly rising, ears locking forward. Camera stays still for the reaction, then begins a small handheld shake as the dog moves.

[00:05-00:10] Shot 2: Low handheld shot following the dog's fast run toward the door, barking implied through the dog's open mouth and body language rather than close mouth detail. Camera moves quickly but stays behind and slightly below the dog, unsteady.

[00:10-00:15] Shot 3: Medium shot, camera at a slight low angle as if from a visitor's point of view, the man crouching to hold the dog by its harness, mouth open as if apologizing repeatedly, visibly straining. Camera holds mostly still with a small handheld wobble. End on the struggle, unresolved.

Negative: no visitor's face shown, no physical contact between dog and any visitor, no bared teeth close-up.
```

---

## V10 · Ladrido reactivo a ruidos del rellano

**Continuidad:** Dog — medium mixed-breed dog, gray-brindle coat. Tutor — woman, 30s, pajamas. Location — apartment hallway, night, dim single light source.

```text
Overall: Very low, dim nighttime lighting, mostly static camera with one handheld burst. Same gray-brindle dog and same woman throughout.

[00:00-00:05] Shot 1: Static close shot on the dog lying in a dark bedroom, ears twitching, body tensing, head lifting slowly. A faint distant sound cue of a bag rustling plays. Camera does not move.

[00:05-00:10] Shot 2: Low handheld shot, camera moves quickly behind the dog as it runs to a hallway and barks at a front door, body language full of tension, facing the door. Camera shake increases with the dog's speed.

[00:10-00:15] Shot 3: Medium shot, the woman in pajamas running barefoot down the hallway, crouching to gently cup the dog's muzzle with both hands, her face tense and pleading. Camera holds mostly still, slight handheld settle as the motion stops. End on her tired, anxious expression.

Negative: no visible neighbors, no exterior hallway shown, no bared teeth close-up.
```

---

## V11 · Tracción desmedida de correa

**Continuidad:** Dog — large mixed-breed dog, tan coat, strong build. Tutor — man, 40s, casual jacket. Location — building entrance and street, bright daytime.

```text
Overall: Bright natural daylight, handheld throughout, energy building steadily across the sequence. Same large tan dog and same man throughout. Leash is a plain fabric leash.

[00:00-00:05] Shot 1: Close shot on a building door opening, street sounds rising (traffic, voices). The dog's eyes dart rapidly between multiple off-screen points, ears swiveling, body coiling with excitement. Camera holds mostly still, small handheld drift.

[00:05-00:10] Shot 2: Low handheld shot from behind, following the man's legs and lower body as the leash pulls taut at a sharp diagonal angle, his torso leaning backward against the pull, feet stumbling slightly on a curb. Camera moves with his uneven gait, unsteady.

[00:10-00:15] Shot 3: Close static shot on the man's hands, faint red marks visible on his palms from the leash. Camera holds completely still. End held on his hands, slightly trembling from exertion.

Negative: no visible cars close to the dog, no other pedestrians in close proximity, no dog off-leash.
```

---

## V12 · Salto impulsivo al saludar

**Continuidad:** Dog — large mixed-breed dog, light golden coat, floppy ears. Tutor — woman, 30s, casual outfit. Neighbor — person in a light-colored jacket, face not emphasized. Location — sidewalk, bright daytime.

```text
Overall: Bright cheerful daylight, upbeat pacing that turns awkward at the end, mostly handheld. Same golden large dog and same woman throughout.

[00:00-00:05] Shot 1: Medium shot, a neighbor in a light jacket stops and leans down slightly, speaking warmly toward the dog. The dog's tail beats hard enough to move its whole hindquarters, back legs coiling to load a jump. Camera holds mostly still.

[00:05-00:10] Shot 2: Slight low-angle handheld shot, camera positioned near the neighbor's shoulder height, the dog springs up, front paws landing on the neighbor's chest, head shaking as if trying to lick their face. Camera absorbs a light jolt of movement with the impact.

[00:10-00:15] Shot 3: Medium shot, the woman pulling the dog down by the collar, mouth open as if repeatedly apologizing, the neighbor brushing dust off their jacket with a strained smile. Camera holds mostly still. End on the woman's embarrassed retreat, looking down.

Negative: no scratches or marks shown on the jacket in close-up, no aggressive dog behavior, no growling implied.
```

---

## V13 · Mordisqueo destructivo en cachorros

**Continuidad:** Dog — puppy, about 3 months old, fluffy brown-and-white coat, oversized paws relative to body. Tutor — man, 20s, casual t-shirt and jeans. Location — living room floor, warm late-afternoon light through a window.

```text
Overall: Warm golden-hour light, intimate and close at the start, turning slightly chaotic mid-sequence, calm and vulnerable at the end. Same fluffy puppy and same young man throughout.

[00:00-00:05] Shot 1: Close static shot, the man sitting cross-legged on the floor, the puppy approaching to lick his fingers gently, tail wagging. Camera holds still.

[00:05-00:10] Shot 2: Close handheld shot, the puppy's mouth closing gently but repeatedly on the man's pant hem and sock, playful tugging motion, the man pulling his foot back quickly. Camera has light handheld movement matching the puppy's quick motions.

[00:10-00:15] Shot 3: Medium shot, the man standing on the sofa, looking down at small scratches on his forearms, his expression shifting from amused to overwhelmed, shoulders dropping, eyes glistening. Camera holds mostly still. End on his tired, emotional expression.

Negative: no blood, no deep wounds, no aggressive adult-dog behavior, puppy proportions must stay consistent (large paws, short legs) across all three shots.
```

---

## V14 · Eliminación inadecuada en interior

**Continuidad:** Dog — medium mixed-breed dog, short black coat, slightly wet from rain. Tutor — woman, 30s, damp raincoat. Location — apartment entryway and living room rug, gray rainy daylight.

```text
Overall: Gray, flat rainy-day light, calm start turning into sudden tension, mostly static camera. Same black medium dog and same woman throughout.

[00:00-00:05] Shot 1: Medium static shot, the woman entering the apartment soaked from rain, removing the dog's harness, then walking off-frame toward another room. The dog remains in frame, sniffing the rug in tight circles.

[00:05-00:10] Shot 2: Static wide shot of the living room, the dog arching its back over the rug in a clearly readable posture. Camera does not move at all, holding the full action in one continuous static take.

[00:10-00:15] Shot 3: Medium shot, the woman re-entering frame, stopping abruptly, hand flying to her forehead, mouth open as if exclaiming loudly. Camera holds mostly still with a small handheld settle. End on her exasperated, exhausted expression.

Negative: no explicit close-up of waste, keep the rug-level action implied by posture and camera distance, no other people in frame.
```

---

## V15 · Zoomies / frenesí vespertino

**Continuidad:** Dog — medium-large mixed-breed dog, energetic build, brown coat. Tutor — man, 30s, home clothes. Location — living room, warm evening lamp light.

```text
Overall: Warm lamp-lit evening light, calm stillness that erupts into fast handheld chaos, then returns to calm stillness. Same brown medium-large dog and same man throughout.

[00:00-00:05] Shot 1: Static close shot, the dog lying down but clearly not relaxed — eyes fixed, mouth slightly open, breathing quickening. Camera holds completely still.

[00:05-00:10] Shot 2: Fast, loose handheld shot following the dog as it leaps onto a sofa, bounces off the backrest, skids across the floor, and grabs a cushion, shaking it hard. Camera moves energetically but stays roughly at the dog's height, deliberately unsteady to convey chaos.

[00:10-00:15] Shot 3: Static high-angle wide shot looking down on the living room, cushions and a rug visibly displaced, the dog now collapsed on the floor in the center of frame, panting, fully still. Camera holds completely static for the full five seconds.

Negative: no broken furniture, no visible damage beyond a torn cushion seam and a displaced rug, no other people in frame.
```

---

## V16 · Ingestión de elementos peligrosos ⚠️

**Continuidad:** Dog — medium mixed-breed dog, white-and-tan coat. Tutor — woman, 40s, casual outdoor clothes. Location — public park, grass and low bushes, overcast daylight.

```text
Overall: Overcast natural daylight, handheld urgency building fast, then a sudden stillness at the end. Same white-and-tan medium dog and same woman throughout. No specific object is shown in detail — keep it generic and unreadable.

[00:00-00:05] Shot 1: Handheld wide shot following the dog's fast, low, purposeful movement through grass toward a dense low bush, nose to the ground the entire time. Camera keeps pace, slightly unsteady.

[00:05-00:10] Shot 2: Close handheld shot on the dog's head at the bush, a quick single swallow motion of the throat, head lifting immediately after. The woman's hand enters frame reaching toward the dog's mouth just as it finishes swallowing — the reach arrives a beat too late. Camera stays close, energetic but controlled.

[00:10-00:15] Shot 3: Low handheld shot, the woman kneeling on the wet grass, staring at her own hands, completely still, her face frozen in uncertainty. Camera holds mostly still with a small handheld settle. End on her stillness, unresolved.

Negative: no visible object identifiable in the dog's mouth, no explicit choking, no visible distress signs beyond stillness and a tense expression, no other people or dogs in the park.
```

---

## Checklist antes de generar

- [ ] Confirmar herramienta de generación real (Veo / Kling / Runway / Sora-class / Hailuo / otra) para saber si el prompt se envía completo (S4) o se parte en 3 prompts S2 encadenados.
- [ ] Generar primero 1–2 vídeos de prueba (p. ej. V01 y V11, los de menor riesgo) para validar consistencia de identidad del perro/tutor entre los 3 segmentos antes de lanzar los 16.
- [ ] VO añadido en posproducción, no generado — grabar o sintetizar aparte.
- [ ] End card de marca añadido en montaje sobre los últimos ~2–3 s del segmento 3, plantilla ya fijada en el guion madre.
- [ ] Revisar cada resultado contra `assets/qc-checklist.md` de la skill `cinematic-director` antes de dar un clip por bueno (Gate 1 aplica al keyframe/primer fotograma si generas con imagen inicial).
- [ ] Los 5 vídeos marcados ⚠️ (V02, V06, V07, V08, V16) llevan CTA suavizado en el end card — no convertir a CTA comercial pleno sin nueva decisión explícita.
