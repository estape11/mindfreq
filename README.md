# mindfreq

> Generador de beats binaurales con presets de ondas cerebrales, visualización en tiempo real y sesiones programadas. Cero dependencias — un solo archivo HTML.

![license](https://img.shields.io/badge/license-MIT-0f62fe)
![zero deps](https://img.shields.io/badge/deps-0-8fab55)
![web audio](https://img.shields.io/badge/Web%20Audio%20API-✓-e9c352)
![single file](https://img.shields.io/badge/single%20file-HTML-474747)

---

## ¿Qué es?

Los beats binaurales se generan cuando cada oído recibe una frecuencia levemente distinta. El cerebro percibe la diferencia como una tercera frecuencia pulsante que tiende a sincronizar la actividad neuronal hacia la banda objetivo (Delta, Theta, Alpha, Beta).

**mind-freq** entrega esos tonos directamente desde el navegador, sin servidores, sin cuentas, sin distractores.

---

## Características

- **5 presets científicamente diseñados**: Concentración (90 min), Relajación (30 min), Anti-estrés (20 min), Meditación (30 min), Sueño (45 min)
- **Modo personalizado**: ajustá frecuencia portadora y beat libremente
- **Visualización canvas**: gráfico de la curva de frecuencia con banda activa destacada y countdown integrado
- **Programación de audio en el reloj del contexto** — las transiciones de frecuencia ocurren aunque el tab esté en segundo plano
- **Fade-out automático** al final de la sesión
- **Duración configurable** con reescalado del schedule del preset
- **Cero dependencias** — HTML/CSS/JS puro, funciona sin conexión

---

## Uso

```bash
# opción 1 — abrir directamente
open index.html

# opción 2 — servir localmente (recomendado para Chrome/Firefox estrictos)
npx serve .
# o
python3 -m http.server 8080
```

> **Importante:** usá audífonos. El efecto binaural requiere canales izquierdo y derecho separados; por parlantes no funciona.

---

## Stack

| Capa | Tecnología |
|---|---|
| Audio | Web Audio API (`AudioContext`, `OscillatorNode`, `StereoPannerNode`) |
| Gráfico | Canvas 2D API |
| UI | HTML/CSS vanilla |
| Dependencias | ninguna |

---

## Presets y ciencia detrás

| Preset | Duración | Portadora | Banda | Rango beat |
|---|---|---|---|---|
| Concentración | 90 min | 150 Hz | Alpha | 10.7–15.2 Hz |
| Relajación | 30 min | 140 Hz | Alpha | 8.5–13 Hz |
| Anti-estrés | 20 min | 144 Hz | Alpha | 10–14 Hz |
| Meditación | 30 min | 136 Hz | Theta | 6–11 Hz |
| Sueño | 45 min | 100 Hz | Delta | 2–10 Hz |

Cada preset define un *schedule* de breakpoints `[minuto, Hz]`. La frecuencia se interpola con una curva coseno-ease para evitar saltos abruptos. Al cambiar la duración de la sesión, el schedule se reescala proporcionalmente.

---

## Estructura del proyecto

```
mindfreq/
└── index.html          # toda la app: markup, estilos y lógica en un solo archivo
```

---

## Contribuir

Ver [CONTRIBUTING.md](CONTRIBUTING.md) para el flujo de trabajo, convenciones de commits y cómo proponer un nuevo preset o feature.

---

## Roadmap

- [ ] Soporte PWA / instalable
- [ ] Timer visual prominente (barra de progreso)
- [ ] Export de preset personalizado como URL compartible (`#custom:150:11:90`)
- [ ] Más presets (creatividad, ADHD, power nap)
- [ ] Modo oscuro / claro
- [ ] Internacionalización (EN / ES)

---

## Licencia

MIT © [estape11](https://github.com/estape11)

---

<p align="center">
  Hecho con 🎧 por <a href="https://github.com/estape11"><strong>estape11</strong></a> · mantenedor principal<br>
  <a href="https://github.com/estape11/mindfreq">github.com/estape11/mindfreq</a>
</p>
