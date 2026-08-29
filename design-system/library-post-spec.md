# Library Post — Design Base

> **Base de diseño de los posts didácticos de la Biblioteca.** Fuente de verdad
> para la skill `.claude/skills/library-post/`. Los tokens NO se copian dentro de
> la skill: se definen aquí y se referencian.

## Fuente de tokens

- **Tokens canónicos:** `design-system/colors_and_type.css` (colores, escala de
  tipos `--text-*`, roles `--h1..--h4`, fuentes, radios, halo de foco).
- **CSS servido en runtime:** `app/public/library/_shared/post.css`. Es un
  **espejo** de los tokens de arriba (Vercel solo sirve lo que hay bajo
  `app/public/`, por eso existe la copia). **Mantener en sync**: si cambia un
  token en `colors_and_type.css`, replicarlo en `_shared/post.css`.
- Cada `styles.css` de post hace `@import url('../_shared/post.css');` y solo
  añade ajustes propios.

## Tipografía — NO inflar

Usar exclusivamente la escala del design-system. Máximos:

| Rol | Token | Tamaño |
|-----|-------|--------|
| h1  | `--text-4xl` | **36px** (tope absoluto) |
| h2  | `--text-3xl` | 28px |
| h3  | `--text-2xl` | 22px |
| h4  | `--text-xl`  | 18px |
| prosa | `--text-lg` (body-lg) | 16px |
| secundario / listas | `--text-base` | 14px |
| mono / badges | `--text-xs` | 11px |

Fuentes: **Space Grotesk** (cuerpo/UI), **JetBrains Mono** (datos/badges). Cargar
por Google Fonts en el `<head>`. **Prohibido** cualquier `font-size` fuera de la
escala (los HTML originales traían 315px/96px — eso NO se replica).

## Color y tema

Claro por defecto, oscuro vía `@media (prefers-color-scheme: dark)` (valores en
`_shared/post.css`). Marca: `--color-primary` `#ef4444`.

## ★ Estados HOVER y ACTIVE (halo de dos niveles) — OBLIGATORIO

Este es el patrón de énfasis **sancionado** del sistema (ver
`colors_and_type.css` §FOCUS/ACTIVE y `preview/components-sidebar.html`). Todo
elemento interactivo (chips, tarjetas clicables, enlaces de navegación, inputs,
selector de idioma) lo respeta:

- **Hover** → **borde 1px rojo** y nada más:
  `border-color: var(--color-primary)`.
- **Active / selected / focus** → **doble borde**: 1px rojo **+ halo**
  translúcido de 4px:
  `border-color: var(--color-primary); box-shadow: 0 0 0 4px rgba(239,68,68,0.25)`
  (`0.18` en claro). Tokens: `--focus-ring` / `--focus-halo`.
- **Prohibido** el borde lateral grueso de acento (ver `design-system/CLAUDE.md`).

Ejemplo ya aplicado: el selector `.lang-switch a.active` lleva el halo. La
excepción es el `.flip` (flip-card): su afordancia es el volteo, no el borde.

## Estructura carpeta-por-post

```
app/public/library/<slug>/
├── es.html            → /library/<slug>/es   (SIEMPRE)
├── en.html            → /library/<slug>/en   (SIEMPRE)
├── styles.css         → @import ../_shared/post.css + ajustes del post
├── script.js          → sella el año; interacción del post (flip, buscador…)
└── assets/
    ├── images/        → imágenes del post
    └── videos/        → vídeos del post
```

`<slug>` = minúsculas, sin espacios, con guiones. Debe coincidir con el `slug`
del item en `library_docs` y en `libraryTaxonomy`/`libraryMockItems`.

## Layout apaisado + aviso de rotación

Los posts se leen mejor en **horizontal**. Al inicio, un banner `.rotate-hint`
(icono SVG de móvil rotando + texto) visible **solo en móvil vertical**
(`@media (orientation: portrait) and (max-width: 820px)`), oculto en horizontal
y escritorio:

- ES: **"Gira la pantalla para una mejor visualización"**
- EN: **"Rotate your screen for a better view"**

## Componentes disponibles (`_shared/post.css`)

Núcleo: `.wrap`, `.rotate-hint`, `.topbar` + `.lang-switch`, `.hero` /
`.eyebrow` / `.lead`, `h1–h4`, `.meta` + `.badge`, `.card`, `.grid` /
`.grid-2` / `.grid-3`, `.num`, `.steps` (jerarquías numeradas), `ul.bul`,
`.quote`, `footer` / `.refs`.

Didácticos: `.type-badge` (CONCEPT/PROCESS/FRAMEWORK/COMPARISON/EXAMPLE/DATA/
PRINCIPLE), `.flip` (flip-card, voltea en hover/tap), `.compare` (A vs B),
`.callout` ("recuerda"). Elegir el componente por tipo y densidad del contenido.

## Categorización y etiquetado (obligatorio)

Cada post se **clasifica por su contenido** en la taxonomía
(`app/src/constants/libraryTaxonomy.ts`):

- **1 categoría** (área de contenido). Si ninguna encaja, **crear una nueva**
  categoría (clave + label ES/EN + descripción + icono Lucide) antes de generar.
- **N etiquetas** de los grupos Disciplina / Nivel / Enfoque / Problema. Si falta
  un término pertinente, **crearlo** en su grupo (o crear un grupo nuevo).
- El `level` (`introductorio|intermedio|avanzado`) se deduce del contenido.

La integración completa (carpeta + taxonomía + fila en `library_docs` vía
migración + entrada mock) la orquesta la skill; ver su `SKILL.md`.
