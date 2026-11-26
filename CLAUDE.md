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
- ID del host en PeerJS: `quiziglesia-<código>`. Servidores ICE en `opcionesPeer()`: STUN de Google + TURN público Open Relay (sin garantía) + TURN propio opcional (config `turnUrl/turnUsuario/turnClave`, sección "Conexión (avanzado)"). Latido: el host envía `ping` cada 5 s, el teléfono responde `pong`; 20 s sin noticias = desconectado (host) / reconexión automática (teléfono). El lobby muestra conectados, "por servidor de respaldo" y "sin señal". El teléfono pide mantener la pantalla encendida (Wake Lock).
- Autoguardado en IndexedDB (`IDB`, clave `actual`; guardado con espera de 400 ms en `guardarLocal()` / inmediato en `guardarAhora()`; localStorage solo como respaldo) + Descargar/Abrir archivo `.quiz.json`. Indicador "Guardado" en la barra del editor y aviso (`aviso()`) si falla.
- Deshacer/rehacer en el editor (`HIST`, hasta 60 pasos, Ctrl+Z / Ctrl+Y / Ctrl+Shift+Z y botones en la barra).
- Filtro de palabras (`tieneGroseria`, `FILTRO_BASE` + `palabrasBloqueadas` de la config): se revisa en el teléfono antes de enviar y otra vez en el host (nombres rechazados con `rechazo`, respuestas groseras quedan vacías). Opción `aprobarNombres` (barra "Por aprobar" en el host). El host puede tocar respuestas de nube y listas para ocultarlas.
- Diapositivas tipo PowerPoint: lienzo 16:9 (`it.fondo` + `it.els`). Elementos texto/imagen/forma con x, y, w, h en % del lienzo; tamaño de letra `fs` en px de un lienzo de 1280 px (CSS con `cqw`). Fondo: color, degradado ("combinar colores", 2–3 colores, lineal/radial, `COMBINACIONES`) o imagen con oscurecer. Diseños predefinidos en `DISENOS`. Las diapositivas del formato antiguo (titulo/texto/imagen/fondo) se convierten con `migrarDiapo()`.
- Galería de fondos: carpeta `fondos/` con 20 imágenes 16:9 generadas en Google Flow (`fondo-01.jpg` … `fondo-20.jpg`, 1365×768, ~100 KB) + `mini/` de miniaturas 384×216, listadas en `fondos/lista.json`. Los prompts están en `fondos/PROMPTS.md` (mismo número que el archivo). El quiz de ejemplo usa fondo-17, 10, 18 y 20. Las rutas son relativas (`fondos/...`): funcionan desde GitHub Pages o con la carpeta junto a index.html.
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
- Sonido (`SND`, Web Audio sin archivos): música de sala de espera y de pregunta, tic en los últimos 5 s, revelar, unirse, redoble (ranking), fanfarria (podio), transición. Config `sonidos` y `musica`; botón silenciar (tecla M) guardado en localStorage.
- Durante la pregunta: pausar (P, congela también los teléfonos), +10 s (+), saltar sin puntaje. Tiempo con `tiempoH()` / `transcurrido()` / `restanteH()`. ← vuelve a la diapositiva anterior (solo diapositivas).
- Control remoto: `?remoto=CODIGO&k=TOKEN` (QR en el modal del host, botón "Nuevo enlace" invalida los anteriores). El host manda `rstate` y recibe `rcmd`.
- Transiciones entre pantallas (config `transicion`, o por diapositiva `it.transicion`): fundido, deslizar, zoom, subir. Animaciones de entrada por elemento (`el.anim`, `el.retraso`). El teléfono vibra al recibir el resultado.
- Host: lobby con QR, sacar jugadores, ranking cada N preguntas, podio final, exportar resultados CSV, modo solo pantalla si no hay conexión.
- Jugador: nombre + avatar emoji, reconexión conservando puntaje (pid en localStorage).

## Probado
- Editor y presentación completos, con jugadores simulados (Playwright, puente directo en vez de PeerJS): todos los tipos, puntaje parcial y modo equipos.
- Editor usable en teléfono (≤ 760 px: lista o formulario, uno a la vez).
- Conexión real por PeerJS probada entre dos páginas del navegador (señalización por 0.peerjs.com).
- Pendiente: probar con teléfonos reales en la red de la iglesia y con datos móviles.

## Ideas siguientes
Sonidos y música de cuenta regresiva.
