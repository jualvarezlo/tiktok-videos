# El 95% Invisible — Videos Verticales (`9:16`)

Serie de explainers animados en HTML5 autocontenidos (formato vertical `9:16` para TikTok, Instagram Reels y YouTube Shorts) dedicada a cuatro físicos colombianos que investigan la materia oscura, la energía oscura y los límites del universo observable:

- **Andrés Plazas Malagón** — Lentes gravitacionales débiles, efecto *brighter-fatter* y la cámara LSST del Observatorio Vera Rubin (SLAC / Stanford).
- **Diego Restrepo** — Masa de los neutrinos, oscilación y mecanismo escotogénico (Universidad de Antioquia).
- **Juan Carlos Sanabria** — El detector CMS del CERN, el bosón de Higgs y la materia oscura supersimétrica (Universidad de los Andes).
- **Leonardo Castañeda** — Gravedad modificada $f(R)$ y el término de frontera en el Observatorio Astronómico Nacional (Universidad Nacional de Colombia).

---

## Videos y Archivos Principales

| Científico | Explainer Interactivo (HTML) | Video MP4 (Con Subtítulos) | Video MP4 (Sin Subtítulos) | Estado de Audio |
| :--- | :--- | :--- | :--- | :--- |
| **Andrés Plazas Malagón** | [`plazas-explainer.html`](plazas-explainer.html) | [`out/plazas-explainer.mp4`](out/plazas-explainer.mp4) | [`out/plazas-explainer-sin-subtitulos.mp4`](out/plazas-explainer-sin-subtitulos.mp4) | Sincronizado (`Narracion/Plazas/plazas-master-mix.mp3`, voz + *Cipher* −15 dB + SFX). Incluye versión [`out/plazas-explainer-solo-voz.mp4`](out/plazas-explainer-solo-voz.mp4). |
| **Diego Restrepo** | [`restrepo-explainer.html`](restrepo-explainer.html) | [`out/restrepo-explainer.mp4`](out/restrepo-explainer.mp4) | [`out/restrepo-explainer-sin-subtitulos.mp4`](out/restrepo-explainer-sin-subtitulos.mp4) | Tiempos estimados (listo para grabar con teleprompter o sincronizar locución). |
| **Juan Carlos Sanabria** | [`sanabria-explainer.html`](sanabria-explainer.html) | [`out/sanabria-explainer.mp4`](out/sanabria-explainer.mp4) | [`out/sanabria-explainer-sin-subtitulos.mp4`](out/sanabria-explainer-sin-subtitulos.mp4) | Tiempos estimados (listo para grabar con teleprompter o sincronizar locución). |
| **Leonardo Castañeda** | [`castaneda-explainer.html`](castaneda-explainer.html) | [`out/castaneda-explainer.mp4`](out/castaneda-explainer.mp4) | [`out/castaneda-explainer-sin-subtitulos.mp4`](out/castaneda-explainer-sin-subtitulos.mp4) | Tiempos estimados (listo para grabar con teleprompter o sincronizar locución). |

### Guion de Lectura en Texto Plano

El discurso completo de los 4 videos (organizado por bloques y con guía de pronunciación) está disponible listo para lectura en voz alta en [`GUION_NARRACION.txt`](GUION_NARRACION.txt).

---

## Estructura del Repositorio

```text
.
├── README.md
├── GUION_NARRACION.txt                 # Guion completo en texto plano para narración
├── plazas-explainer.html               # Explainer interactivo de Andrés Plazas (con audio sincronizado)
├── restrepo-explainer.html             # Explainer interactivo de Diego Restrepo
├── sanabria-explainer.html             # Explainer interactivo de Juan Carlos Sanabria
├── castaneda-explainer.html            # Explainer interactivo de Leonardo Castañeda
├── Narracion/
│   └── Plazas/                         # Tomas originales (.m4a), voz limpia y mezcla maestra (.mp3)
├── out/                                # Renders finales MP4 (1080×1920, 30 fps) y hoja de contacto
├── recursos-externos/
│   ├── 00_investigacion/               # Dossiers biográficos, conceptos y verificación factual
│   └── 02_assets/                      # Retratos, archivo público, gráficos, música y SFX
│       ├── INDICE_DE_ASSETS.md
│       ├── INSTRUCTIVO_ASSETS_Y_LICENCIAS.md
│       └── licencias.csv
└── .agents/skills/explainer/           # Motor, referencias y scripts (simular.cjs, render.mjs, palabras.mjs)
```

---

## Cómo Usar los Explainers en el Navegador

Cada archivo `*-explainer.html` es una aplicación interactiva en Canvas 2D con subtítulos karaoke sincronizados y panel de guion lateral.

- **Reproducir / Pausar:** Toca el centro del cuadro o presiona `Espacio` (en `plazas-explainer.html` arranca en pausa para permitir la reproducción de audio en el navegador).
- **Navegar entre escenas:** Toca los laterales izquierdo/derecho, usa las flechas `←` / `→`, o haz clic en cualquier bloque del panel **Guion**.
- **Modo grabación (`H`):** Presiona **Modo grabación** o la tecla `H` para ocultar controles y barras de progreso y reiniciar desde `00:00`.
- **Subtítulos y barras (`S`):** Presiona el interruptor o la tecla `S` para ocultar/mostrar subtítulos y barras superiores.
- **Reiniciar (`R`):** Vuelve al segundo `0`.
- **Previsualizar otro formato:** Añade `?formato=16:9`, `?formato=1:1` o `?formato=4:5` a la URL del archivo HTML.

---

## Simulación y Exportación a Video (CLI)

El proyecto utiliza los scripts de [`.agents/skills/explainer/scripts/`](.agents/skills/explainer/scripts/) con Node.js, Playwright (Chromium) y FFmpeg.

### 1. Instalar dependencias (solo la primera vez)

```bash
cd .agents/skills/explainer/scripts
npm install
npx playwright install chromium
```

### 2. Validar lógica y sincronía en todos los formatos

```bash
node .agents/skills/explainer/scripts/simular.cjs plazas-explainer.html --todos
```

### 3. Generar hojas de contacto o exportar MP4

```bash
# Hoja de contacto con el cuadro final de cada escena
node .agents/skills/explainer/scripts/render.mjs plazas-explainer.html --fotos finales

# Exportar video a 1080×1920 y 30 fps (con subtítulos)
node .agents/skills/explainer/scripts/render.mjs plazas-explainer.html --fps 30

# Exportar video sin subtítulos (para edición externa)
node .agents/skills/explainer/scripts/render.mjs plazas-explainer.html --fps 30 --query bare=1 --nombre plazas-explainer-sin-subtitulos
```

> **Nota sobre pistas `.wav`:** Para respetar los límites de tamaño de archivo de GitHub, los archivos `.wav` sin comprimir de música y locución están excluidos en `.gitignore`; sus equivalentes `.mp3` de alta calidad están incluidos en el repositorio y pueden reconvertirse a WAV con `recursos-externos/02_assets/musica/convertir_mp3_a_wav.mjs` o `ffmpeg`.

---

## Fuentes Científicas y Licencias

- **Investigación y verificación de datos:** [`recursos-externos/00_investigacion/fact_check_report.md`](recursos-externos/00_investigacion/fact_check_report.md)
- **Catálogo y licencias de activos visuales y sonoros:** [`recursos-externos/02_assets/INDICE_DE_ASSETS.md`](recursos-externos/02_assets/INDICE_DE_ASSETS.md), [`recursos-externos/02_assets/INSTRUCTIVO_ASSETS_Y_LICENCIAS.md`](recursos-externos/02_assets/INSTRUCTIVO_ASSETS_Y_LICENCIAS.md) y [`recursos-externos/02_assets/licencias.csv`](recursos-externos/02_assets/licencias.csv).
- **Música de fondo:** *Cipher* (Kevin MacLeod, incompetech.com), licencia Creative Commons BY 4.0.
