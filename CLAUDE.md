# Quiz Iglesia — contexto del proyecto

App web tipo Kahoot para la iglesia, pensada para niños y adolescentes. Combina diapositivas con rondas de preguntas.

## Requisitos del usuario
- Sin base de datos: el quiz se guarda y se abre como archivo `.json` (las imágenes van incrustadas en base64).
- Parametrizable (configuración general + por pregunta).
- Participantes que se unen desde el teléfono (QR + código de 5 dígitos).
- Muchos tipos de pregunta, no solo alternativas y V/F.
- Publicado en GitHub Pages: https://adda-santiago.github.io/Quiz/ (repo adda-santiago/Quiz, rama `main`).
- Idioma de la interfaz y del código: español.

## Estado actual (v1)
- Todo está en un solo archivo: `index.html` (HTML + CSS + JS vanilla, sin build).
- Dependencias por CDN: PeerJS 1.5.4 (WebRTC, conexión teléfono ↔ pantalla, sin servidor propio) y qrcode-generator 1.4.4.
- Diseño visual: sistema "Sanctuary Tech" del proyecto de Google Stitch "Interactive Church Quiz Redesign" (pantallas Inicio y Pregunta, escritorio y celular). Tokens como variables CSS en `:root` (primario índigo #180157, cian #006780, magenta #A21CAF, dorado #F59E0B, fondo #FDF8FF). Fuentes de Google Fonts: Instrument Serif (títulos y preguntas), Instrument Sans (texto), Source Code Pro (códigos y números) e íconos Material Symbols Outlined (helper `ic(nombre)`). Sin Tailwind: CSS propio.
- Alternativas con letras A–F (`LETRAS`) y los colores de `COLORES`; V/F con V verde y F roja. En el teléfono se responde con un solo toque.
- Vistas: Inicio, Editor, Presentar (host), Jugador (`?join=CODIGO`).
- ID del host en PeerJS: `quiziglesia-<código>`.
- Autoguardado en localStorage + Descargar/Abrir archivo `.quiz.json`.
- Tipos implementados: diapositiva, alternativas, vf, completar, pin, ordenar, numero, parejas, versiculo, quiensoy, revela, clasificar, error, emoji, linea, encuesta, nube, escala.
  - `emoji` y `revela` reutilizan opciones de colores (`CON_OPCIONES` / `CON_CORRECTAS`).
  - `error`: la palabra equivocada se marca entre *asteriscos* en el texto.
  - `versiculo`: se corta por palabras, o por trozos si el texto tiene "/".
  - `linea`: lista cronológica + índice `ubicar` del hecho que hay que ubicar.
  - Sin puntaje: encuesta, nube, escala.
- Puntaje: puntos base × multiplicador (normal/doble/sin puntos), bonus por velocidad opcional (hasta −50 %).
  - `fraccion(it, v)` devuelve 0–1: parejas y clasificar dan puntaje parcial ("¡Casi!" en el teléfono).
  - ¿Quién soy?: el puntaje depende de cuántas pistas había visibles (no del tiempo). Imagen que se revela: siempre con bonus por velocidad.
- Modo equipos (config `modoEquipos` + `nombresEquipos`): se elige equipo en el lobby desde el teléfono; ranking, podio y CSV por equipo (suma de integrantes).
- Al presentar, `problemasQuiz()` avisa de preguntas incompletas.
- Host: lobby con QR, sacar jugadores, ranking cada N preguntas, podio final, exportar resultados CSV, modo solo pantalla si no hay conexión.
- Jugador: nombre + avatar emoji, reconexión conservando puntaje (pid en localStorage).

## Probado
- Editor y presentación completos, con jugadores simulados (Playwright, puente directo en vez de PeerJS): todos los tipos, puntaje parcial y modo equipos.
- Editor usable en teléfono (≤ 760 px: lista o formulario, uno a la vez).
- Pendiente: probar conexión real con teléfonos (PeerJS) una vez publicado.

## Ideas siguientes
Sonidos y música de cuenta regresiva.
