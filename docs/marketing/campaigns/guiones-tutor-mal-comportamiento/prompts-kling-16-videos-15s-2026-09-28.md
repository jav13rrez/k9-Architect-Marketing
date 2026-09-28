# K9 Architect — 16 prompts Kling, listos para pegar (15 s)

**Sustituye a** `prompts-ia-16-videos-15s-2026-09-28.md` (ese fichero era genérico y no seguía el pipeline real de la skill — se deja como referencia narrativa, no como prompts de producción).

**Herramienta:** Kling 可灵. **Idioma de los prompts: chino** — es lo que exige el adaptador de Kling en `references/ai-video-tool-adapters.md` para mejor resultado; un prompt en inglés es una traducción que el modelo tiene que deshacer primero. Cada bloque chino es **lo que se pega tal cual** en Kling. Al lado, una glosa en español (no un segundo prompt) para que puedas verificar el contenido sin depender de traducción.

## Cómo está construido (Mode E + Mode F reales, no genéricos)

- **Forma:** S1 (imagen→vídeo desde un keyframe) para los planos 1 y 3 de cada vídeo; **S3 (par primer+último fotograma)** para el plano 2, el de mayor riesgo de cada escena — es la recomendación explícita de la skill para el plano más difícil.
- **Cadena de 3 clips de ~5 s = 15 s**, corte duro en montaje. El end card de marca se añade en posproducción, no se genera.
- **负向提示 (campo de negativos) es real en Kling** — todo lo que se excluye va ahí, nunca como negación dentro del prompt positivo (una negación dentro del prompt en Kling puede invocar lo que nombra).
- **Identity strings** de cada perro y tutor siguen la receta de `continuity-bible.md`: 30–50 palabras, hechos físicos fijos + un único rasgo distintivo comprobable + un ancla de "vestuario" (collar/correa en el perro). Se pegan **verbatim**, nunca parafraseadas.
- **NEG_BASE compartido** por los 16 (instancias, no categorías):

```text
NEG_BASE (负向提示): 人脸变化，服装改变，多余的手指，变形的爪子，画面闪烁，抖动，文字，水印，第二只狗，镜头角度突然切换
Glosa: face change, costume change, extra fingers, deformed paws, flicker, jitter, text, watermark, second dog, sudden angle change
```

- **Contacto de riesgo (mordida):** el plano 2 (S3) siempre termina *antes* del contacto — el segundo frame es el instante justo anterior, nunca el contacto en sí. Es más fiable para el modelo y es la misma decisión de bienestar del guion madre.
- **VO y end card:** no se generan con Kling. VO se dobla aparte; end card es plantilla de marca añadida en montaje.

---

## V01 · Reactividad por frustración

**ID_PERRO:** `棕黄色中大型混种犬，短毛，竖立的三角耳，天然短尾，尾尖快速抖动，脖子上系着一条深灰色布质牵引绳`
*(perro mediano-grande, pelo corto tostado, orejas triangulares erguidas, cola natural corta vibrando, correa de tela gris oscura)*

**ID_TUTOR:** `30岁女性，深色马尾扎起，鹅蛋脸，右手手背有一道浅色旧疤，身穿深棕色雨衣，衣领竖起`
*(mujer 30 años, coleta oscura, cicatriz clara en el dorso de la mano derecha, gabardina marrón oscuro con cuello subido)*

**LOCK:** `狭窄的欧洲老城人行道，磨损的灰色铺路石，背景停着几辆自行车，阴天`
**LIGHT:** `阴天散射光，无明显阴影方向，色温偏冷`

### Plano 1 (S1) — desencadenante

```text
镜头 1 关键帧。远景，平视，机位1.5米，35mm。棕黄色中大型混种犬，短毛，竖立的三角耳，天然短尾，脖子上系着深灰色布质牵引绳；30岁女性，深色马尾，深棕色雨衣，衣领竖起，右手握着牵引绳。二人站在狭窄石板人行道上，25米外另一只犬平静经过。犬只身体僵直，尾尖开始颤动，双耳前倾。女性手腕下意识将牵引绳缠紧一圈。阴天散射光，无方向性阴影。9:16。
负向提示：人脸变化，服装改变，多余的手指，变形的爪子，文字，水印，第二只犬只清晰面部特写
```

```text
镜头 1 动态。固定镜头，不做任何移动。犬只保持躯干僵直，尾尖持续快速抖动约一秒，随后前爪离地半步，喉部发出一次低哼（无需画面表现声音）。女性的右手缓慢将牵引绳再缠紧半圈，手指关节发白。结尾停在：犬只前爪刚触地，身体前倾15度，绳索绷直。同一张脸，同一件雨衣，同一只犬。
负向提示：人脸变化，服装改变，画面闪烁，抖动，文字，水印
```
*Glosa: plano fijo. El perro tensa el cuerpo, vibra la punta de la cola, empieza a alzar las patas delanteras; la mujer aprieta el puño sobre la correa. Termina con el perro inclinado 15° hacia delante, correa tensa.*

### Plano 2 (S3, par primer+último fotograma) — manifestación

```text
关键帧A（首帧）。中景，平视，机位1.2米，50mm。同一只犬（体貌与镜头1一致），前爪已离地，身体前倾45度，绳索呈45度斜线绷紧，口部微张但未发出吠叫。同一位女性，双脚后撤半步以对抗拉力，双手紧握绳索。阴天散射光。9:16。
负向提示：人脸变化，服装改变，第二只犬，文字，水印

关键帧B（尾帧）。同景别、同机位、同镜头。犬只四脚落地，身体后仰喘息，舌头侧垂，眼神涣散。女性肩膀下垂，绳索松弛下垂。同一张脸，同一件雨衣，同一只犬。
负向提示：人脸变化，服装改变，第二只犬，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。从首帧过渡到尾帧：犬只完成一次向前跃起又落地的动作，绳索始终未松脱，另一只犬已离开画面。运动集中在后半段完成，前段几乎静止。镜头固定，不摇不移。保持同一张脸、同一件雨衣、同一只犬、同一牵引绳。
负向提示：人脸变化，服装改变，画面闪烁，第二只犬清晰入镜，文字，水印
```
*Glosa: par de fotogramas. Primero = perro en el aire tirando a 45°. Último = perro con las cuatro patas en el suelo, jadeando, correa floja. El movimiento se concentra en la segunda mitad, arranque casi estático.*

### Plano 3 (S1) — desenlace

```text
镜头 3 关键帧。特写，平视，机位0.9米，85mm。同一只犬，舌头侧垂喘息，眼神涣散，背景虚化为灰色人行道。9:16。
负向提示：人脸变化，多余的手指，文字，水印

镜头 3 动态。固定镜头。犬只胸腔起伏加快后逐渐放缓，喘气频率降低，眼神从涣散到略微聚焦。结尾停在：犬只闭上嘴，喘息平稳。
负向提示：画面闪烁，抖动，文字，水印
```
*Glosa: primer plano del perro jadeando, la respiración se calma progresivamente hasta cerrar la boca.*

**Montaje:** clip1 (5s) + clip2 (5s, del par) + clip3 (5s) = 15s. End card overlay sobre los últimos 2s de clip3: `K9 ARCHITECT / Un paso cada vez. / Probar con mi perro / Aplicación web · 7 días sin tarjeta`.

---

## V02 · Reactividad por miedo ⚠️

**ID_PERRO:** `中型黑白花色混种犬，短毛，圆耳下垂，鼻梁处有一小块白色斑纹，脖子上系着黑色细牵引绳`
**ID_TUTOR:** `40岁男性，短络腮胡，深蓝色羽绒外套，左眉有一道浅疤`
**陌生人（背景，不需清晰面部）:** `身穿米色厚外套的行人`

**LOCK:** `同类型狭窄人行道，转角处视线受阻`
**LIGHT:** `阴天散射光，冷色调`

### Plano 1 (S1)

```text
镜头 1 关键帧。特写，平视，机位0.6米，85mm。中型黑白花色犬，鼻梁白斑，圆耳，快速舔鼻，身体重心后移，颈部黑色牵引绳绷直。9:16。
负向提示：人脸变化，牙齿外露，文字，水印

镜头 1 动态。固定镜头。犬只连续舔鼻两次，耳朵微微压低，后腿弯曲试图后退，牵引绳始终绷直阻止后退。结尾停在：犬只重心完全后移但被绳索拉住，身体僵直。
负向提示：牙齿外露，画面闪烁，文字，水印
```
*Glosa: el perro se lame el hocico, intenta retroceder, la correa tensa se lo impide. Termina con el cuerpo rígido, sin poder huir.*

### Plano 2 (S3) — máximo riesgo, corte antes del contacto

```text
关键帧A（首帧）。中景，平视，机位1.5米，50mm。40岁男性，深蓝羽绒外套，左眉疤痕，惊讶表情初现，身体开始后仰；犬只在画面下方边缘，仅露出后半身，不露口部。9:16。
负向提示：牙齿外露，血迹，第二人清晰面部，文字，水印

关键帧B（尾帧）。同景别同机位。男性手臂完全向后甩开，身体后仰45度，惊恐表情。犬只已不在画面内（已跑出画面下方）。
负向提示：牙齿外露，血迹，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。男性手臂从自然下垂猛然向后甩出，身体重心后仰，表情从平静瞬间转为惊恐，全程不露出犬只口部或牙齿——冲突本身发生在画面之外，仅通过男性的反应呈现。镜头固定不移动。
负向提示：牙齿外露，血迹，伤口，画面闪烁，文字，水印
```
*Glosa: el conflicto ocurre fuera de cuadro — solo vemos la reacción del hombre (brazo que se retira de golpe, cuerpo hacia atrás). El perro y su boca nunca están en plano en este segmento.*

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.3米，50mm。陌生人身体前倾，表情警觉；男性一手护住自己手臂，另一手做道歉手势。9:16。
负向提示：血迹，伤口特写，文字，水印

镜头 3 动态。固定镜头。男性反复做道歉手势（手掌张开向下压两次），陌生人后退半步。结尾停在：两人保持1米距离，男性手掌仍张开。
负向提示：血迹，画面闪烁，文字，水印
```

**Nota:** end card de este vídeo debe llevar CTA suavizado (derivación/profesional), no alta directa — coherente con el guion madre.

---

## V03 · Ansiedad por separación — pánico vocal

**ID_PERRO:** `中型金棕色混种犬，长耳下垂，毛质柔软`
**ID_TUTOR:** `20多岁女性，齐肩直发，米色针织衫，帆布手提袋`

**LOCK:** `小型公寓玄关，木门，黄铜门把手，墙上挂钩`
**LIGHT:** `单一暖色台灯光源，室内偏暗`

### Plano 1 (S1)

```text
镜头 1 关键帧。近景，平视，机位1.4米，50mm。20多岁女性，齐肩直发，米色针织衫，右手举起正从挂钩取下一串钥匙；中型金棕色犬蹲坐在她脚边，瞳孔放大，微微喘气。暖色台灯光源。9:16。
负向提示：人脸变化，服装改变，第二只犬，文字，水印

镜头 1 动态。固定镜头。女性手中钥匙串轻轻摇晃一次，随后蹲下用双手捧住犬只脸颊；犬只呼吸频率加快，身体贴近女性小腿。结尾停在：女性双手仍捧着犬只脸颊，二者视线相对。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。远景，平视，机位1.5米，35mm。木门从内侧关闭的瞬间，门缝可见钥匙插入痕迹；犬只不在画面内。9:16。
负向提示：文字，水印，人物入镜

关键帧B（尾帧）。同景别同机位。犬只前爪搭在门把手下方的木门上，身体拉伸向上，门板出现轻微抓痕。
负向提示：门损坏过度，血迹，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。从空门到犬只扑门：犬只从画面外冲入，两次前爪搭门的跳跃动作，后爪落地又再次跃起，门把手下方木纹出现浅色抓痕。镜头固定。
负向提示：门损坏过度，血迹，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。远景，平视，机位1.6米，35mm。空荡荡的走廊，木门在画面中景，无人物。9:16。
负向提示：人物入镜，文字，水印

镜头 3 动态。固定镜头，全程不移动。画面保持完全静止5秒，仅通过留白传达门后的持续声响（后期配音）。
负向提示：任何物体移动，画面闪烁，文字，水印
```
*Glosa: pasillo vacío, cámara completamente quieta — el silencio visual es la pieza clave, el sonido se añade en posproducción.*

---

## V04 · Ansiedad por separación — destructividad

**ID_PERRO:** `中大型深色虎斑混种犬，短毛，粗壮体型`（solo aparece en plano 1）
**ID_TUTOR:** `30多岁男性，休闲短袖衬衫，短发`

**LOCK:** `公寓客厅，木质门框，百叶窗，墙上挂钟`
**LIGHT:** `午后光线渐暗至傍晚，暖色台灯逐渐成为主光源`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.5米，35mm。客厅全景，木质门框未受损，墙上挂钟指向某一时刻，深色虎斑犬站在门边。午后光线。9:16。
负向提示：人脸变化，第二只犬，文字，水印

镜头 1 动态。固定镜头。灯光在5秒内极缓慢地从午后色温过渡到暖黄色台灯光，模拟数小时流逝；犬只在画面中静止站立后走出画面。结尾停在：空房间，只有挂钟和门框，暖黄灯光。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S1，无犬只入镜——物件动画)

```text
镜头 2 关键帧。特写，平视，机位0.4米，85mm。木质门框底部，完好无损，木纹清晰可见。9:16。
负向提示：动物入镜，文字，水印

镜头 2 动态。固定镜头，画面中始终不出现任何动物。门框底部木材表面在5秒内逐渐出现啃咬痕迹：木屑一片片剥落堆积，边缘出现齿痕状凹陷。结尾停在：门框底部明显破损，木屑散落在地。
负向提示：动物入镜，血迹，文字，水印
```
*Glosa: ningún animal en cuadro en ningún momento — solo animación del objeto dañándose, evita cualquier riesgo de bienestar en la generación.*

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.4米，50mm。30多岁男性站在打开的门口，表情尚平静，手搭在门把手上。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头。男性视线下移，嘴巴张开呈惊讶状，一只手抬起捂住嘴，肩膀微微下沉。结尾停在：男性手捂嘴，视线固定在地面。
负向提示：画面闪烁，文字，水印
```

---

## V05 · Fobia acústica

**ID_PERRO:** `老年小中型混种犬，口鼻部分毛发发白，毛色灰棕`
**ID_TUTOR:** `50多岁女性，居家便装，灰白挽起的头发`

**LOCK:** `公寓窗边转走廊到卫生间`
**LIGHT:** `夜晚冷色调，低照度`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.5米，35mm。窗外乌云密布，室内昏暗，老年灰棕色犬尚未入镜或位于画面边缘。9:16。
负向提示：人物入镜，文字，水印

镜头 1 动态。固定镜头，不移动。远处闪电一次（画面轻微增亮），随后犬只（口鼻发白）从画面边缘转头望向窗户，身体僵直。结尾停在：犬只完全僵立，望向窗外。
负向提示：画面闪烁过度，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。中景，平视，机位0.5米（低机位），50mm。老年犬在走廊中段，耳朵后压，身体低伏，四肢准备发力。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。同景别，机位改为紧贴地面0.3米。犬只已挤入卫生间柜子旁狭窄缝隙，身体大部分被遮挡，仅露出后半身，肌肉可见轻微震颤。
负向提示：夸张震颤，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只从走廊中段低伏姿态，快速移动至卫生间狭窄缝隙处并挤入，动作急促但轨迹清晰单一。镜头贴地跟随，轻微手持感但不剧烈晃动。
负向提示：夸张震颤，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.2米，50mm。冷色调卫生间，50多岁女性坐在地上，怀中轻抱着颤抖的老年犬。9:16。
负向提示：人脸变化，夸张震颤，文字，水印

镜头 3 动态。固定镜头，全程5秒不移动。犬只身体保持轻微、自然幅度的颤抖，女性双臂环抱姿势不变。
负向提示：画面闪烁，夸张动作，文字，水印
```

---

## V06 · Protección de recursos con comida ⚠️

**ID_PERRO:** `中型棕色壮实犬，短毛，宽头型`
**ID_TUTOR:** `30多岁男性，居家短袖`
**道具:** `无品牌标识的压制骨状咬胶`

**LOCK:** `客厅地毯旁的犬床`
**LIGHT:** `柔和日间光线`

### Plano 1 (S1)

```text
镜头 1 关键帧。中景，平视，机位1.3米，50mm。棕色壮实犬安静卧在犬床上，前爪间夹着骨状咬胶，正在啃咬。柔和日光。9:16。
负向提示：人脸变化，第二只犬，文字，水印

镜头 1 动态。固定镜头。男性双脚从画面右侧缓慢进入，步伐正常，逐渐靠近犬床。结尾停在：男性双脚停在距犬床约2米处。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3) — máximo riesgo

```text
关键帧A（首帧）。特写，俯拍15度，机位0.6米，85mm。犬只眼球侧转露出眼白（鲸眼），头部低压覆盖咬胶，身体完全僵直不动。9:16。
负向提示：牙齿外露，文字，水印

关键帧B（尾帧）。中景，平视，机位1.2米，50mm。男性手臂向后猛然撤回，手指张开，身体后仰，脸部惊讶表情初现；犬只低头咬住咬胶，未露出牙齿细节。
负向提示：牙齿外露，血迹，接触瞬间，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。男性手臂从自然伸出状态在最后一刻猛然撤回，全程手掌与犬只口部保持可见距离、不发生接触，动作在极短时间内完成并定格在撤回姿态。
负向提示：接触瞬间，牙齿外露，血迹，画面闪烁，文字，水印
```
*Glosa: la mano se retira de golpe SIN llegar a tocar; el contacto nunca se muestra, solo el instante justo anterior y el instante justo posterior.*

### Plano 3 (S1)

```text
镜头 3 关键帧。特写，平视，机位0.7米，85mm。犬只正快速吞咽咬胶，喉部可见吞咽动作。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头。犬只完成吞咽动作后抬头，男性手臂在画面边缘虚焦处仍保持后撤姿势。结尾停在：犬只咬胶已完全吞下，嘴部闭合。
负向提示：画面闪烁，文字，水印
```

**Nota:** CTA suavizado en end card — «con un profesional delante», no alta directa.

---

## V07 · Protección de recursos sobre mobiliario/tutor ⚠️

**ID_PERRO:** `中型奶油色犬，中长毛`
**ID_TUTOR A (dueña):** `40多岁女性，居家便装`
**ID_TUTOR B (familiar):** `40多岁男性，居家便装`

**LOCK:** `客厅沙发，晚间`
**LIGHT:** `暖色台灯光源`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.4米，35mm。奶油色犬蜷缩睡在沙发上，紧贴40多岁女性；40多岁男性从画面一侧走入，走向沙发。暖色灯光。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头。男性持续走近沙发直至距离约1米处停下，犬只眼睛在最后一刻突然睁开。结尾停在：男性站定，犬只双眼圆睁望向他。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。特写，平视，机位0.6米，85mm。犬只下颌明显收紧绷直，身体完全不动，眼睛直视前方。9:16。
负向提示：牙齿外露，文字，水印

关键帧B（尾帧）。中景，平视，机位1.3米，50mm。女性身体前倾，一手前伸做保护性手势，表情转为警觉；男性和犬只仅在画面边缘小幅可见，动态模糊，细节不清。
负向提示：牙齿外露，血迹，接触瞬间，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。女性从平静坐姿快速前倾并伸出一只手臂，表情从放松转为警觉，全程画面焦点始终在女性身上；男性和犬只之间的互动仅作为画面边缘的模糊动作暗示，不做清晰呈现。
负向提示：牙齿外露，接触瞬间清晰呈现，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.3米，50mm。女性独自面对镜头方向，表情紧张而复杂。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头。女性缓慢眨眼一次，嘴唇微微抿紧，肩膀轻微下沉。结尾停在：女性表情定格，目光低垂。
负向提示：画面闪烁，文字，水印
```

**Nota:** CTA suavizado — informe/ajuste del profesional.

---

## V08 · Agresividad por dolor físico oculto ⚠️

**ID_PERRO:** `老年中型犬，口鼻周围毛发发白，步态略显僵硬`
**ID_TUTOR:** `50多岁女性，居家便装，袖子挽起`

**LOCK:** `客厅地毯，雨天`
**LIGHT:** `透过雨痕玻璃窗的灰色日光`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.4米，35mm。老年犬卧在地毯上，毛发略湿；50多岁女性手持毛巾跪坐在旁。灰色雨天光线。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头。女性用毛巾轻柔擦拭犬只后腿及髋部区域，动作缓慢温柔；犬只呼吸在某一瞬间短暂停顿，双耳略微后压。结尾停在：毛巾停留在髋部区域，犬只耳朵仍处于后压状态。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。中景，平视，机位1.2米，50mm。女性前臂正接触犬只髋部，动作温柔，犬只身体尚未有明显反应。9:16。
负向提示：牙齿外露，文字，水印

关键帧B（尾帧）。特写，平视，机位0.8米，85mm。女性手臂猛然撤回，另一只手护住手腕，表情震惊；不显示任何伤口或血迹细节。
负向提示：伤口，血迹，牙齿外露，接触瞬间，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。女性手臂从温柔擦拭的姿态在极短时间内猛然向后甩开，表情从平静瞬间转为震惊，全程不展示犬只口部与手臂的接触细节，冲突通过女性的反应呈现。
负向提示：伤口，血迹，牙齿外露，接触瞬间，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。特写，平视，机位0.9米，85mm。女性低头看着自己的手腕，手腕处无可见伤口，表情震惊而困惑。9:16。
负向提示：伤口，血迹，文字，水印

镜头 3 动态。固定镜头。女性另一只手轻轻捧住受影响的手腕，眼睛缓慢眨动一次。结尾停在：双手交叠护在胸前，表情定格。
负向提示：画面闪烁，文字，水印
```

**Nota:** CTA final = derivación veterinaria explícita, es el eje del vídeo.

---

## V09 · Ladrido de alarma ante visitas

**ID_PERRO:** `大型黑色犬，短毛，三角耳直立敏锐`
**ID_TUTOR:** `30多岁男性，居家便装`

**LOCK:** `公寓玄关，木门，猫眼`
**LIGHT:** `午后柔和室内光`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.5米，35mm。安静客厅，大型黑色犬侧卧休息，30多岁男性坐在沙发上。柔和午后光。9:16。
负向提示：人脸变化，第二只犬，文字，水印

镜头 1 动态。固定镜头。犬只在极短时间内从卧姿弹起至完全站立，背部毛发沿脊柱方向竖起，双耳锁定朝向门的方向。结尾停在：犬只四肢站立，身体朝向门，毛发竖起状态定格。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。远景，平视，机位1.3米，35mm。犬只从客厅冲向玄关途中，身体呈奔跑姿态，四肢腾空。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。中景，仰拍10度（模拟访客视角），机位1.0米，50mm。犬只已到达门边，前身压低，口部张开呈吠叫姿态但不露出獠牙特写。
负向提示：獠牙特写，第二人入镜，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只从客厅中段全速奔向玄关门口，途中步伐节奏清晰可数（四步），到达门边后身体前压定格在吠叫准备姿态。镜头低机位手持跟拍，轻微自然晃动。
负向提示：獠牙特写，第二人清晰入镜，画面闪烁过度，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位0.8米（蹲姿高度），50mm。30多岁男性蹲下，双手扶住犬只胸背部挽具，表情紧张。9:16。
负向提示：人脸变化，第二人入镜，文字，水印

镜头 3 动态。固定镜头，轻微手持。男性嘴部反复张合做道歉手势状，身体因用力保持犬只而略微晃动。结尾停在：男性双手仍稳稳扶住挽具，姿态维持不变。
负向提示：画面闪烁过度，文字，水印
```

---

## V10 · Ladrido reactivo a ruidos del rellano

**ID_PERRO:** `中型灰虎斑犬，中等体型`
**ID_TUTOR:** `30多岁女性，居家睡衣`

**LOCK:** `公寓走廊，深夜`
**LIGHT:** `极低照度，单一微弱光源`

### Plano 1 (S1)

```text
镜头 1 关键帧。特写，平视，机位0.6米，85mm。黑暗卧室中，灰虎斑犬卧姿，一只耳朵开始抽动，头部缓慢抬起。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头，全程极暗环境。犬只耳朵持续抽动两次，头部完全抬起，身体逐渐绷紧。结尾停在：犬只完全清醒坐姿，双耳竖起。
负向提示：画面过曝，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。远景，低机位0.5米，35mm。犬只在黑暗走廊中奔跑姿态，朝向大门方向。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。中景，平视，机位0.9米，50mm。犬只已到达门边，正对门缝，身体绷紧，口部张开吠叫姿态定格。
负向提示：獠牙特写，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只从走廊中段快速奔向大门，到达后正对门缝定格吠叫姿态。镜头低机位手持跟随，晃动幅度随犬只速度增加而增大。
负向提示：獠牙特写，画面过曝，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.0米，50mm。30多岁女性赤脚跑至走廊，蹲下双手轻捧犬只口鼻部，表情焦虑。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头，轻微手持余震后趋于稳定。女性双手保持轻柔捧住犬只口鼻的姿态，肩膀因跑动残留轻微起伏后逐渐平稳。结尾停在：二者静止，女性表情疲惫而专注。
负向提示：画面闪烁，文字，水印
```

---

## V11 · Tracción desmedida de correa

**ID_PERRO:** `大型棕黄色壮实犬，短毛，体格强壮`
**ID_TUTOR:** `40多岁男性，休闲夹克`

**LOCK:** `建筑入口到街道`
**LIGHT:** `明亮日间自然光`

### Plano 1 (S1)

```text
镜头 1 关键帧。特写，平视，机位1.2米，85mm。建筑木门刚打开一条缝，大型棕黄色犬的头部探出，眼球快速左右转动。明亮日光。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头。犬只双眼在多个方向间快速扫视，双耳来回转动，后腿肌肉可见蓄力收紧。结尾停在：犬只身体前倾蓄势，即将迈步。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。特写（腿部与绳索），俯拍20度，机位0.8米，50mm。深灰色牵引绳呈45度斜线绷紧，男性身体重心后仰对抗拉力。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。同景别，机位与角度一致。男性双脚在路缘石处踉跄失衡，身体倾斜幅度增大，绳索角度不变。
负向提示：摔倒在地，画面闪烁，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。绳索保持45度绷紧状态不变，男性身体因犬只持续拉力而重心不稳，在路缘石处踉跄一步但未跌倒，动作幅度逐渐增大。镜头低机位手持跟拍腿部。
负向提示：摔倒在地，画面闪烁过度，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。特写，平视，机位0.5米，85mm。男性双手掌心可见浅红色勒痕，手指微微颤抖。9:16。
负向提示：血迹，皮肤破损，文字，水印

镜头 3 动态。固定镜头，全程静止。双手因用力残留的颤抖逐渐平息。结尾停在：双手完全静止，勒痕清晰可见。
负向提示：画面闪烁，血迹，文字，水印
```

---

## V12 · Salto impulsivo al saludar

**ID_PERRO:** `大型浅金色犬，垂耳，中长毛`
**ID_TUTOR:** `30多岁女性，休闲装`
**邻居（背景）:** `身穿浅色外套的路人，面部不做特写`

**LOCK:** `人行道，晴天`
**LIGHT:** `明亮日光`

### Plano 1 (S1)

```text
镜头 1 关键帧。中景，平视，机位1.3米，50mm。浅色外套邻居微微俯身，正对大型浅金色犬说话；犬只尾巴摆动幅度极大带动臀部左右摇摆。9:16。
负向提示：人脸变化，第二只犬，文字，水印

镜头 1 动态。固定镜头。犬只后腿持续弯曲蓄力，尾巴摆动频率加快，身体重心下沉准备起跳。结尾停在：犬只后腿完全弯曲蓄势，即将跃起。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。中景，仰拍10度（邻居肩部高度），机位1.1米，50mm。犬只四肢离地，身体呈跃起姿态，尚未接触邻居。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。同景别同机位。犬只前爪已搭在邻居胸前衣物上，头部微微摆动做亲昵姿态，未露出獠牙。
负向提示：獠牙特写，抓伤特写，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只从跃起腾空姿态过渡到前爪搭在邻居胸前的落地瞬间，头部随之摆动一次做亲昵姿态。镜头承受轻微冲击式晃动模拟撞击感。
负向提示：抓伤特写，獠牙特写，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.2米，50mm。女性一手拉住犬只项圈向下，嘴部张开呈道歉状；邻居一手拍打衣物上的灰尘。9:16。
负向提示：人脸变化，抓痕特写，文字，水印

镜头 3 动态。固定镜头。女性反复做道歉手势（点头两次），邻居持续拍打衣物三次后停止。结尾停在：女性视线低垂后退半步。
负向提示：画面闪烁，文字，水印
```

---

## V13 · Mordisqueo destructivo en cachorros

**ID_PERRO (cachorro):** `3个月大幼犬，棕白双色蓬松毛发，耳朵偏大，爪子明显偏大`
**ID_TUTOR:** `20多岁男性，居家T恤牛仔裤`

**LOCK:** `客厅地板`
**LIGHT:** `温暖傍晚阳光，逆光`

### Plano 1 (S1)

```text
镜头 1 关键帧。中景，平视，机位1.0米，50mm。20多岁男性盘腿坐在地板上，3个月大棕白幼犬正靠近舔舐他的手指，尾巴摇摆。温暖逆光。9:16。
负向提示：人脸变化，成犬体型，文字，水印

镜头 1 动态。固定镜头。幼犬持续舔舐手指约两秒后，瞳孔突然放大，口鼻开始快速小幅抽动。结尾停在：幼犬嘴部已张开，准备咬握动作。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。特写，平视，机位0.5米，85mm。幼犬牙齿轻轻咬住男性裤脚边缘，尾巴仍在摇摆，无攻击性表现。9:16。
负向提示：血迹，成犬牙齿，文字，水印

关键帧B（尾帧）。中景，平视，机位1.1米，50mm。男性站立在沙发上，双臂前伸保持平衡，表情又惊又笑；幼犬在地面仰头望向他，仍保持幼犬体型。
负向提示：血迹，伤口特写，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。幼犬持续小幅度拉扯裤脚（三次轻拽），男性脚部向后收回，随后整个身体快速站上沙发，双臂前伸保持平衡。幼犬体型与比例（大耳大爪短腿）全程保持一致。
负向提示：成犬比例，血迹，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.2米，50mm。男性站在沙发上低头看着自己前臂，表情从惊讶转为疲惫，眼眶微湿。9:16。
负向提示：人脸变化，血迹，文字，水印

镜头 3 动态。固定镜头。男性肩膀缓慢下沉，头部略微低垂，一只手轻轻抹过眼角。结尾停在：男性低头静止，肩膀完全放松下垂。
负向提示：画面闪烁，文字，水印
```

---

## V14 · Eliminación inadecuada en interior

**ID_PERRO:** `中型黑色短毛犬，毛发略湿`
**ID_TUTOR:** `30多岁女性，湿透的雨衣`

**LOCK:** `公寓玄关到客厅地毯`
**LIGHT:** `灰色阴雨天光线`

### Plano 1 (S1)

```text
镜头 1 关键帧。中景，平视，机位1.3米，50mm。30多岁女性浑身湿透站在玄关，正给中型黑色犬解下胸背带；灰色阴雨光线。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头。女性完全解下挽具后转身走出画面；犬只留在原地，鼻子贴近地毯快速画圈嗅闻两次。结尾停在：犬只背部微微拱起，准备排泄姿态。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S1，无需过渡对，单一静态长镜头)

```text
镜头 2 关键帧。远景，平视，机位1.4米，35mm。客厅全景，地毯居中，犬只背部拱起姿态清晰但不做排泄物细节呈现。9:16。
负向提示：排泄物特写，人物入镜，文字，水印

镜头 2 动态。固定镜头，全程5秒完全不移动，不切镜。犬只维持背部拱起姿态约2秒后恢复自然站姿。结尾停在：犬只恢复正常站姿，画面保持原有构图。
负向提示：排泄物特写细节，画面闪烁，文字，水印
```
*Glosa: la acción se implica por la postura, no por un primer plano explícito — encuadre a distancia deliberado.*

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，平视，机位1.3米，50mm。女性重新进入客厅画面，脚步突然停止，一只手抬起按向额头。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头。女性嘴部张大呈喊叫状一次，随后肩膀垮下呈疲惫姿态。结尾停在：女性双肩下垂，手仍按在额头。
负向提示：画面闪烁，文字，水印
```

---

## V15 · Zoomies / frenesí vespertino

**ID_PERRO:** `中大型棕色犬，精瘦肌肉型体格`
**ID_TUTOR:** `30多岁男性，居家便装`

**LOCK:** `客厅`
**LIGHT:** `傍晚暖色台灯`

### Plano 1 (S1)

```text
镜头 1 关键帧。特写，平视，机位0.7米，85mm。棕色犬卧姿但眼神固定不放松，嘴部微张，呼吸频率略快。暖色台灯光。9:16。
负向提示：人脸变化，文字，水印

镜头 1 动态。固定镜头，全程静止。犬只呼吸频率在5秒内持续加快，身体从卧姿逐渐绷紧至蓄势欲起。结尾停在：犬只四肢收拢在身下，随时准备弹起。
负向提示：画面闪烁，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。远景，平视，机位1.2米，35mm。犬只跃上沙发瞬间，四肢腾空，靠垫开始移位。9:16。
负向提示：人脸变化，文字，水印

关键帧B（尾帧）。同景别同机位。犬只叼住一个靠垫用力甩动，地毯已明显移位，靠垫接缝处出现裂口。
负向提示：家具损坏，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只从沙发跃起经过背靠反弹，沿地板高速滑行后叼住靠垫用力甩动数次。镜头手持跟随犬只高度，晃动幅度大但保持犬只主体清晰。
负向提示：家具严重损坏，画面闪烁过度，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。俯拍45度，机位2.2米（高机位俯瞰），24mm。客厅全景俯视，靠垫和地毯明显移位，犬只瘫倒在画面中央地面。9:16。
负向提示：家具严重损坏，文字，水印

镜头 3 动态。固定镜头，全程静止5秒不移动。犬只胸腔起伏明显但幅度逐渐减小，身体完全瘫软不动。结尾停在：犬只完全静止，仅胸腔轻微起伏。
负向提示：画面闪烁，文字，水印
```

---

## V16 · Ingestión de elementos peligrosos ⚠️

**ID_PERRO:** `中型白棕双色犬，中等体型`
**ID_TUTOR:** `40多岁女性，户外休闲装`

**LOCK:** `公园草地，灌木丛`
**LIGHT:** `阴天散射日光`

### Plano 1 (S1)

```text
镜头 1 关键帧。远景，平视，机位1.0米（跟拍高度），35mm。白棕双色犬鼻子贴地，正快速穿过草地朝密集灌木丛移动。阴天光线。9:16。
负向提示：人脸变化，可辨识物体，文字，水印

镜头 1 动态。手持跟拍，机位随犬只移动。犬只保持鼻贴地面的姿态快速直线移动至灌木丛边缘，步伐加快。结尾停在：犬只头部已伸入灌木丛边缘。
负向提示：画面闪烁过度，可辨识危险物体特写，文字，水印
```

### Plano 2 (S3)

```text
关键帧A（首帧）。特写，平视，机位0.5米，85mm。犬只头部在灌木丛前，口部尚未闭合，喉部尚未有吞咽动作。9:16。
负向提示：可辨识物体特写，文字，水印

关键帧B（尾帧）。同景别同机位。犬只头部已完全抬起离开灌木丛，喉部刚完成一次吞咽动作，女性一只手正伸入画面但已错过时机。
负向提示：可辨识物体特写，窒息表现，文字，水印
```

```text
镜头 2 动态（首尾帧过渡）。犬只完成一次快速吞咽动作后头部立即抬起离开灌木丛，与此同时女性的手从画面外伸入试图触碰犬只口部但慢了一步。全程不展示被吞咽物体的清晰细节。
负向提示：可辨识危险物体，窒息表现，画面闪烁，文字，水印
```

### Plano 3 (S1)

```text
镜头 3 关键帧。中景，低机位0.6米，50mm。40多岁女性跪在湿草地上，双手摊开望着自己的手掌，表情凝固茫然。9:16。
负向提示：人脸变化，文字，水印

镜头 3 动态。固定镜头，全程静止5秒不移动。女性保持跪姿凝望双手，仅眼睛缓慢眨动一次。结尾停在：完全静止，表情不变。
负向提示：画面闪烁，文字，水印
```

**Nota:** CTA final = derivación de urgencia veterinaria explícita, es el eje del vídeo.

---

## Checklist de validación antes de generar en Kling

- [ ] Confirmar que el negativo se pega en el **campo 负向提示 real de Kling**, no dentro del prompt positivo — es donde este adaptador dice que Kling lo soporta de verdad.
- [ ] Generar primero **V01 y V11** (menor riesgo, mecánica física simple) para validar que Kling mantiene la identidad del perro y del tutor entre los 3 planos antes de lanzar los 16.
- [ ] Para cada par de keyframes (S3), generar y aprobar **ambos fotogramas como imagen fija primero** — el gate de la skill es explícito: "vídeo nunca repara un error de keyframe, lo anima". No generar vídeo sobre un keyframe que no hayas mirado.
- [ ] Revisar identidad (raza/tamaño/color/orejas) en el primer, plano medio y último fotograma de cada clip generado — no solo en la miniatura.
- [ ] Después de generar: 对口型 y audio no aplican aquí (no hay diálogo generado, VO en posproducción) — no actives lip-sync.
- [ ] Los 5 vídeos ⚠️ (V02, V06, V07, V08, V16) mantienen CTA suavizado en el end card, añadido en montaje.
