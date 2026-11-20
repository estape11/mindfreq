# CLAUDE.md — mindfreq

Contexto para sesiones de desarrollo asistidas por IA.

---

## Qué es este proyecto

**mindfreq** — generador de beats binaurales en el navegador. Cero dependencias, un solo archivo (`index.html`). Desplegado en GitHub Pages: https://estape11.github.io/mindfreq/

Repositorio: https://github.com/estape11/mindfreq

---

## Arquitectura

```
index.html   ← toda la app: HTML + CSS + JS en un archivo
README.md
CONTRIBUTING.md
CLAUDE.md
```

No hay build step, bundler, ni package.json. Nunca agregar dependencias externas — la app debe seguir siendo un único archivo autocontenido.

---

## Stack

| Capa | Tecnología |
|---|---|
| Audio | Web Audio API (`AudioContext`, `OscillatorNode`, `StereoPannerNode`) |
| Gráfico | Canvas 2D API |
| UI | HTML/CSS vanilla |
| Deploy | GitHub Pages (branch `main`, raíz `/`) |

---

## Convenciones de commits

Seguimos [Conventional Commits](https://www.conventionalcommits.org/). Tipos usados en este repo:

| Tipo | Uso |
|---|---|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `style` | CSS / visual sin cambio funcional |
| `preset` | Nuevo preset o ajuste de schedule |
| `refactor` | Reorganización sin efecto externo |
| `docs` | README, CONTRIBUTING, CLAUDE.md |
| `chore` | Mantenimiento |

Siempre agregar al final del commit:
```
Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
```

---

## Flujo de trabajo

```bash
# rama
git checkout -b feature/<resumen-en-kebab-case>

# commit
git commit -m "feat(alcance): descripción imperativa"

# push y deploy automático vía GitHub Pages
git push
```

No hay CI — el push a `main` despliega directamente.

---

## Estado del proyecto (nov 2026)

### Implementado
- 5 presets con schedules de frecuencia: concentración (90min), relajación (30min), anti-estrés (20min), meditación (30min), sueño (45min)
- Modo personalizado (frecuencia portadora + beat libres)
- Canvas con gráfico de la curva de frecuencia, bandas coloreadas y countdown
- Animación de resplandor en el punto de progreso (onda seno 3.5s)
- Scrubbing — click o drag en el canvas para saltar a cualquier minuto
- Programación de audio en el reloj del `AudioContext` (funciona con tab en background)
- Fade-out automático al fin de sesión
- Modal "¿Cómo funciona?" con ciencia, bandas cerebrales y 4 referencias PubMed
- Footer con hash del commit en runtime (fetch a GitHub API)
- Mobile: `min-height: 100dvh`, safe-area, controles en columna, modal como bottom sheet
- GitHub Pages activo

### Roadmap pendiente
- PWA / instalable
- Timer visual (barra de progreso)
- URL compartible con preset custom (`#custom:150:11:90`)
- Más presets (power nap, creatividad, ADHD)
- Modo oscuro / claro

---

## Variables CSS

```css
--bg: #5b84a3          /* fondo azul */
--card-dark: #474747   /* tarjetas */
--card-dark-shadow: #3a3a3a
--green: #8fab55       /* beat activo, play */
--green-shadow: #75904a
--yellow: #e9c352      /* banda Beta, links en modal */
--ink: #ffffff
```

---

## Lógica de audio clave

- `carrier` — frecuencia portadora en Hz (oído izquierdo)
- `carrier + beatAt(min)` — oído derecho
- `beatAt(min)` — interpola el schedule con coseno-ease
- `scheduleAudio()` — programa toda la sesión restante en el AudioContext; llamar después de cualquier cambio de frecuencia, seek o play
- `restartClock()` — resetea `elapsedMs = 0` y llama `scheduleAudio()`

## Lógica del canvas

- `layout()` — recalcula `W`, `H`, `plot` al resize; llamar si se agrega algo que cambie el tamaño
- `draw()` — dibuja todo; corre en cada frame de `requestAnimationFrame`
- `plot = { x, y, w, h }` — área de graficado en píxeles CSS
- `xOf(min)` / `yOf(hz)` — conversión coordenadas

---

## Mantenedor principal

**estape11** — https://github.com/estape11
