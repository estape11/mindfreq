# Guía de contribución — mindfreq

> Aplica tanto a aportes humanos como a aportes asistidos por IA.

Inspirado en las convenciones de [Examentico](https://github.com/estape11/examentico) y alineado con los estándares de la industria:
- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/)
- [Keep a Changelog 1.1.0](https://keepachangelog.com/)
- [Semantic Versioning 2.0.0](https://semver.org/)

---

## Principios generales

1. **`main` es intocable.** Todo cambio entra por Pull Request.
2. **Un issue, una rama, un PR.** Cada PR responde a exactamente un problema o feature.
3. **Sin dependencias externas.** La app debe seguir siendo un solo archivo HTML autocontenido.
4. **El audio no puede romperse.** Cualquier cambio que afecte `Web Audio API` requiere prueba manual con audífonos.
5. **Documentar la decisión.** El mensaje de commit y la descripción del PR responden: *si aplico este cambio, qué resultado obtengo y por qué*.

---

## Flujo de trabajo

### 1. Antes de empezar

1. Sincronizá `main`:
   ```bash
   git checkout main && git pull
   ```
2. Buscá o creá el issue correspondiente en GitHub. Sin issue no hay PR.

### 2. Crear la rama

```bash
git checkout -b <accion>/<resumen>
```

| Prefijo | Uso |
|---|---|
| `feature/` | Funcionalidad nueva |
| `update/` | Mejora sobre funcionalidad existente |
| `fix/` | Corrección de bug |
| `preset/` | Nuevo preset de brainwaves |
| `refactor/` | Reorganización sin cambio funcional |
| `docs/` | Solo documentación |

**Reglas:**
- Resumen en kebab-case, ≤ 40 caracteres
- Nombrar el resultado, no el proceso: `feature/url-compartible`, no `feature/agregando-url-compartible`

**Ejemplos válidos:**
- `feature/pwa-support`
- `preset/power-nap`
- `fix/canvas-resize-dpr`
- `update/fade-out-duration`
- `docs/preset-science`

### 3. Desarrollar

- Trabajá en commits pequeños y autocontenidos.
- Probá en Chrome y Firefox con audífonos reales antes de abrir el PR.
- Si modificás un preset existente, documentá los cambios en el PR con capturas del gráfico antes/después.
- Si agregás un preset nuevo, incluí la fuente o referencia científica/bibliográfica del schedule.

### 4. Mantener la rama al día

```bash
git fetch origin
git rebase origin/main
git push --force-with-lease
```

> Siempre `--force-with-lease`, nunca `--force` a secas.

### 5. Abrir el PR

```bash
gh pr create \
  --title "feat(preset): power nap de 20 minutos" \
  --base main \
  --head preset/power-nap
```

- El título sigue el formato de Conventional Commits (ver sección siguiente).
- Linkear el issue con `Closes #N` o `Refs #N` (si el PR es trabajo parcial).

---

## Convención de commits

Seguimos [Conventional Commits 1.0.0](https://www.conventionalcommits.org/).

```
<tipo>(<alcance>): <descripción en imperativo, minúscula, sin punto final>

[cuerpo opcional: qué y por qué, no cómo]

[pie opcional: Closes #N, Breaking change, Co-Authored-By, etc.]
```

### Tipos

| Tipo | Cuándo usarlo |
|---|---|
| `feat` | Nueva funcionalidad visible al usuario |
| `fix` | Corrección de bug |
| `preset` | Nuevo preset o ajuste de schedule |
| `refactor` | Cambio sin efecto externo |
| `style` | Solo CSS / formato visual |
| `docs` | README, CONTRIBUTING, comentarios |
| `chore` | Tareas de mantenimiento (`.gitignore`, etc.) |

### Alcances sugeridos

`audio`, `chart`, `ui`, `preset`, `controls`, `a11y`, `pwa`

### Ejemplos

```
feat(audio): programar frecuencias en el reloj del AudioContext

Evita que las transiciones se pierdan cuando el tab queda en background.
requestAnimationFrame se congela; AudioContext.currentTime no.

Closes #12
```

```
preset(sleep): ajustar rampa inicial de 10 a 8 Hz

Los primeros 4 minutos eran demasiado abruptos según feedback.
Refs #18
```

```
fix(chart): corregir DPI en pantallas retina

El canvas usaba clientWidth sin multiplicar por devicePixelRatio.
Closes #7
```

---

## Proponer un nuevo preset

Un preset nuevo debe incluir:

1. **Nombre y objetivo** (ej. "Power nap — recuperación rápida en 20 min")
2. **Portadora (`carrier`)** en Hz
3. **Banda objetivo** (Delta / Theta / Alpha / Beta)
4. **Schedule** como array de breakpoints `[minuto, Hz]`
5. **Duración base** en minutos
6. **Referencia**: paper, libro o fuente que sustente el schedule (no es obligatorio citar un estudio con DOI, pero sí indicar la base)

Abrí primero un issue del tipo *Preset proposal* antes de implementar, para discutir el schedule y evitar trabajo duplicado.

---

## Estilo de código

- **Vanilla JS** — sin frameworks, sin transpiladores, sin bundlers.
- Variables y funciones en `camelCase`.
- Constantes de configuración en `SCREAMING_SNAKE_CASE` en el bloque superior del `<script>`.
- Sin comentarios obvios — solo comentarios que expliquen *por qué*, no *qué*.
- Máximo 120 caracteres por línea.
- Indentación: 2 espacios.

---

## Reportar un bug

Incluí en el issue:
- **Descripción breve** del comportamiento incorrecto
- **Pasos para reproducir**
- **Comportamiento esperado**
- **Entorno**: navegador + versión, OS, tipo de audio (auriculares, parlantes)
- **Captura o grabación** si aplica

---

## Mantenedor principal

**[estape11](https://github.com/estape11)** — PRs y issues son revisados normalmente dentro de los 7 días hábiles.

---

<p align="center">
  <a href="https://github.com/estape11/mindfreq">github.com/estape11/mindfreq</a>
</p>
