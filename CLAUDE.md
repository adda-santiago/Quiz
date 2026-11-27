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
- Dependencias por CDN: PeerJS 1.5.4 (WebRTC, conexión teléfono ↔ pantalla, sin servidor propio) y qrcode-generator 1.4.4; bajo demanda JSZip 3.10.1 y pdf.js 3.11.174 (cdnjs) para importar PowerPoint/PDF.
- Diseño visual: sistema "Sanctuary Tech" del proyecto de Google Stitch "Interactive Church Quiz Redesign" (pantallas Inicio y Pregunta, escritorio y celular). Tokens como variables CSS en `:root` (primario índigo #180157, cian #006780, magenta #A21CAF, dorado #F59E0B, fondo #FDF8FF). Fuentes de Google Fonts: Instrument Serif (títulos y preguntas), Instrument Sans (texto), Source Code Pro (códigos y números) e íconos Material Symbols Outlined (helper `ic(nombre)`). Sin Tailwind: CSS propio.
- Alternativas con letras A–F (`LETRAS`) y los colores de `COLORES`; V/F con V verde y F roja. En el teléfono se responde con un solo toque.
- Vistas: Inicio, Editor, Presentar (host), Jugador (`?join=CODIGO`).
- ID del host en PeerJS: `quiziglesia-<código>`. Servidores ICE en `opcionesPeer()`: STUN de Google + TURN público Open Relay (sin garantía) + TURN propio opcional (config `turnUrl/turnUsuario/turnClave`, sección "Conexión (avanzado)"). Latido: el host envía `ping` cada 5 s, el teléfono responde `pong`; 20 s sin noticias = desconectado (host) / reconexión automática (teléfono). El lobby muestra conectados, "por servidor de respaldo" y "sin señal". El teléfono pide mantener la pantalla encendida (Wake Lock).
- Autoguardado en IndexedDB (`IDB`, clave `actual`; guardado con espera de 400 ms en `guardarLocal()` / inmediato en `guardarAhora()`; localStorage solo como respaldo) + Descargar/Abrir archivo `.quiz.json`. Indicador "Guardado" en la barra del editor y aviso (`aviso()`) si falla.
- Deshacer/rehacer en el editor (`HIST`, hasta 60 pasos, Ctrl+Z / Ctrl+Y / Ctrl+Shift+Z y botones en la barra).
- Filtro de palabras (`tieneGroseria`, `FILTRO_BASE` + `palabrasBloqueadas` de la config): se revisa en el teléfono antes de enviar y otra vez en el host (nombres rechazados con `rechazo`, respuestas groseras quedan vacías). Opción `aprobarNombres` (barra "Por aprobar" en el host). El host puede tocar respuestas de nube y listas para ocultarlas.
- Diapositivas tipo PowerPoint: lienzo 16:9 (`it.fondo` + `it.els`). Elementos texto/imagen/forma con x, y, w, h en % del lienzo; tamaño de letra `fs` en px de un lienzo de 1280 px (CSS con `cqw`). Fondo: color, degradado ("combinar colores", 2–3 colores, lineal/radial, `COMBINACIONES`) o imagen con oscurecer. Diseños predefinidos en `DISENOS`. Las diapositivas del formato antiguo (titulo/texto/imagen/fondo) se convierten con `migrarDiapo()`.
- Video de YouTube en diapositivas (elemento `t:'video'`, `ytId()`): en el editor muestra la miniatura; en la presentación un iframe de youtube-nocookie con `enablejsapi=1`, controlado por postMessage (`comandoVideo`: botón Reproducir/Pausar, tecla K, control remoto). `renderHost()` no reemplaza el escenario si la diapositiva tiene video (para no recargarlo). Aviso `AVISO_YT` sobre anuncios en el editor y en la barra.
- Galería de fondos: carpeta `fondos/` con 20 imágenes 16:9 generadas en Google Flow (`fondo-01.jpg` … `fondo-20.jpg`, 1365×768, ~100 KB) + `mini/` de miniaturas 384×216, listadas en `fondos/lista.json`. Clasificadas: `lista.json` = `{ categoriasFondo, historias (58, AT/NT con pasaje), imagenes: [{archivo, mini, nombre, tipo: 'fondo'|'historia', categoria?, historias?}] }` (acepta también el arreglo antiguo). La galería (`galeriaHTML(accion, actual)`, filtro `GAL`, `refrescarGalerias`) filtra Todas/Fondos (por categoría)/Historias (por historia) en el fondo de diapositiva, el fondo de la presentación y `elegirImagen()`. Los prompts están en `fondos/PROMPTS.md` (mismo número que el archivo). El quiz de ejemplo usa fondo-17, 10, 18 y 20. Las rutas son relativas (`fondos/...`): funcionan desde GitHub Pages o con la carpeta junto a index.html.
- Tipos implementados (28): diapositiva, alternativas, vf, completar, pin, ordenar, numero, parejas, versiculo, quiensoy, revela, clasificar, error, emoji, linea, huecos, multiple, rafaga, palabra, zoom, audio, memoria, rapido, dibujo, muro, encuesta, nube, escala.
  - `emoji`, `revela`, `zoom` y `audio` reutilizan las opciones A–F (`CON_OPCIONES` / `CON_CORRECTAS`).
  - `parejas`: cada lado puede tener texto (`a`/`b`) e imagen (`ai`/`bi`); en el teléfono se unen arrastrando o tocando (`iniciarUniones`, líneas SVG). Respuesta: `v[k]` = índice original de la pareja elegida para la izquierda k.
  - `revela`: matriz configurable (`cols`, `filas`), `pasos` (0 = uno por cuadro) e `intervalo` en s (0 = automático según el tiempo); ver `gridRevela()` / `cuadrosQuitados()`.
  - Selector de imagen `elegirImagen()`: subir desde el equipo o elegir de la galería de fondos (preguntas, elementos de diapositiva y parejas).
  - `huecos`: frase con varios ___ + banco de palabras (correctas en orden + distractores), puntaje parcial.
  - `multiple`: marcar todas las correctas (cada correcta suma, cada incorrecta resta).
  - `rafaga`: afirmaciones V/F de a una en el teléfono; `palabra`: letras que aparecen de a una (menos letras = más puntos).
  - `zoom`: imagen que parte ampliada en (zx, zy) y se aleja; `audio`: se reproduce en la pantalla (`H.audio`), sin música de fondo.
  - `memoria`: cartas en el teléfono; `rapido`: botón en el teléfono, fila `H.cola`, el presentador marca ✔/✘ (`H.ganador`).
  - `dibujo` (canvas → JPEG) y `muro` (opción `moderar`, el presentador aprueba): sin puntaje, se ven en vivo (`EN_VIVO`).
  - Progreso parcial: el teléfono manda `prog` (memoria, ráfaga); si se acaba el tiempo, `revelar()` lo cuenta como respuesta.
  - Filtro de palabras solo en `TEXTO_LIBRE` (completar, nube, quiensoy, palabra, muro).
  - `error`: la palabra equivocada se marca entre *asteriscos* en el texto.
  - `versiculo`: se corta por palabras, o por trozos si el texto tiene "/".
  - `linea`: lista cronológica + índice `ubicar` del hecho que hay que ubicar.
  - Sin puntaje: encuesta, nube, escala, dibujo, muro.
- Puntaje: puntos base × multiplicador (normal/doble/sin puntos), bonus por velocidad opcional (hasta −50 %).
  - `fraccion(it, v)` devuelve 0–1: parejas y clasificar dan puntaje parcial ("¡Casi!" en el teléfono).
  - ¿Quién soy?: el puntaje depende de cuántas pistas había visibles (no del tiempo). Imagen que se revela: siempre con bonus por velocidad.
- Modo equipos (config `modoEquipos` + `nombresEquipos` + `asignarEquipos`: 'elegir' | 'aleatorio' (equilibrado) | 'llegada'; `asignarEquipo()`, botón "Mezclar equipos" en el lobby): ranking, podio y CSV por equipo (suma de integrantes).
- Aviso de cookies (`avisoCookies()`, acciones globales en `GLOBAL`): la primera vez en Inicio, jugador y control remoto (nunca en el proyector ni en navegadores automatizados); el tutorial espera a que se acepte.
- Editor de diapositivas en escritorio (≥ 1150 px): lienzo a la izquierda y panel de formato fijo a la derecha. En el pin y el zoom el punto se arrastra (`arrastrarPunto`).
- Al presentar, `problemasQuiz()` avisa de preguntas incompletas.
- Sonido (`SND`, Web Audio sin archivos): música de sala de espera y de pregunta, tic en los últimos 5 s, revelar, unirse, redoble (ranking), fanfarria (podio), transición. Config `sonidos` y `musica`; botón silenciar (tecla M) guardado en localStorage.
- Durante la pregunta: pausar (P, congela también los teléfonos), +10 s (+), saltar sin puntaje. Tiempo con `tiempoH()` / `transcurrido()` / `restanteH()`. ← vuelve a la diapositiva anterior (solo diapositivas).
- Control remoto: `?remoto=CODIGO&k=TOKEN` (QR en el modal del host, botón "Nuevo enlace" invalida los anteriores). El host manda `rstate` y recibe `rcmd`.
- Transiciones entre pantallas (config `transicion`, o por diapositiva `it.transicion`): fundido, deslizar, zoom, subir. Animaciones de entrada por elemento (`el.anim`, `el.retraso`). El teléfono vibra al recibir el resultado.
- "Mis quizzes": cada quiz tiene `id`; se guarda en IDB como `q:<id>` + índice `indice` (`INDICE`, `guardarEnIndice`, `cambiarQuiz`). Lista en el Inicio (abrir, duplicar, eliminar). "Quiz en blanco" y "Cargar ejemplo" crean quizzes nuevos sin borrar el actual.
- Vista previa en el editor: dos iframes de la misma app (`?vista=host` y `?vista=jugador`) que reciben el quiz por `postMessage` (`vistaPrevia()`), con navegación y fase pregunta/respuesta.
- Importar PowerPoint (`abrirImportarPpt`): pregunta el modo y luego muestra miniaturas para elegir qué diapositivas importar (`mostrarSeleccion`; las ocultas vienen desmarcadas). «Como elementos editables» lee el .pptx con JSZip (`importarPptx`): textos (tamaño/color/negrita/alineación/viñetas, estilos del patrón y colores del tema), imágenes y formas simples quedan editables; **gráficos** (dibujados con sus datos en canvas: `dibujarGrafico` — columnas/barras, apiladas, líneas, áreas, torta, anillo, dispersión), **tablas**, **SmartArt** (dibujo guardado en `ppt/diagrams/drawing*.xml`), **líneas** y **figuras especiales/formas libres** (SVG: `geomSVG`, `POLIGONOS`) se convierten en imagen (marcados `_pdf`). Opcional: con el PDF exportado del mismo PowerPoint, esos elementos se recortan del PDF (`recortarConPdf`, admite PDF sin las diapositivas ocultas). «Como imágenes» usa el PDF (pdf.js) o imágenes sueltas. Librerías bajo demanda (`LIBS`, `cargarScript`).
- Exportar a PDF (`abrirExportarPdf` → `prepararImpresion(modo, conDiapos)`): pregunta modo pregunta o modo respuesta (respuesta marcada + `textoCorrecta` al pie), opción de incluir diapositivas. Una hoja 1280×720 por elemento, tal como se ve en la pantalla grande (`hostPregunta` con un `H` falso, `H.imprimir`; `IMPRIMIENDO` muestra miniatura en videos). Vista previa `#impresion` y luego `window.print()` («Guardar como PDF»); CSS `@media print` con `@page{size:1280px 720px}`. Botones en Inicio, barra del editor y menú ⋮.
- Importar preguntas (`parsearImportacion`): texto (alternativas con *, V/F, =respuesta, lista numerada para ordenar, varias * → marca todas), tabla pegada de Excel/Sheets (Pregunta · Correcta · Otras) o JSON. `PROMPT_IA()` genera el prompt para pedírselas a una IA.
- Fondo de la presentación (`config.fondoPres`): color, degradado o imagen de la galería detrás de preguntas, sala de espera y ranking (el contenido va sobre un panel claro).
- Tutorial guiado (`TOURS`, `tour()`): Inicio y Editor, se abre solo la primera vez (no en navegadores automatizados) y con el botón ❓.
- Idiomas (`config.idioma`: 'es' | 'en' | 'me' montenegrino latino; selector en Configuración): traduce la pantalla de presentación, el teléfono, el control remoto, el aviso de cookies del teléfono y el PDF; el editor queda en español. `tr('texto en español', {vars})` + diccionario `I18N` (lista [es, en, me]), `IDIOMA`, `ponerIdioma()`, `nombreTipo()`. El teléfono recibe el idioma en `welcome`; antes de conectarse usa `&l=` del QR (`urlUnirse`/`urlRemoto`), el último guardado (`quiziglesia.idioma`) o el del navegador (`idiomaInicialTel`). Las preguntas no se traducen.
- Añadir pregunta: botón desplegable fijo (sticky) arriba de «Configuración» en la lista del editor (`menuAdd`), tipos agrupados en `GRUPOS_TIPOS`; descripción de cada tipo en `DESC_TIPOS` (globo flotante `#tipTipo` al pasar el mouse en escritorio, texto bajo el nombre en el teléfono).
- Editor en teléfono: barra con ←, deshacer, rehacer, vista previa, presentar y menú ⋮ (guardar, abrir, importar, tutorial); el título va en una segunda fila.
- Host: lobby con QR, sacar jugadores, ranking cada N preguntas, podio final, exportar resultados CSV, modo solo pantalla si no hay conexión.
- Jugador: nombre + avatar emoji, reconexión conservando puntaje (pid en localStorage).

## Probado
- Editor y presentación completos, con jugadores simulados (Playwright, puente directo en vez de PeerJS): todos los tipos, puntaje parcial y modo equipos.
- Editor usable en teléfono (≤ 760 px: lista o formulario, uno a la vez).
- Conexión real por PeerJS probada entre dos páginas del navegador y **por el usuario con teléfonos reales** (como participante y como control remoto): funciona.

## Ideas siguientes
Sonidos y música de cuenta regresiva.
