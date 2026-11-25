# Quiz Iglesia — contexto del proyecto

App web tipo Kahoot para la iglesia, pensada para niños y adolescentes. Combina diapositivas con rondas de preguntas.

## Requisitos del usuario
- Sin base de datos: el quiz se guarda y se abre como archivo `.json` (las imágenes van incrustadas en base64).
- Parametrizable (configuración general + por pregunta).
- Participantes que se unen desde el teléfono (QR + código de 5 dígitos).
- Muchos tipos de pregunta, no solo alternativas y V/F.
- Se publicará en GitHub Pages (el usuario ya usa crist-alarc.github.io).
- Idioma de la interfaz y del código: español.

## Estado actual (v1)
- Todo está en un solo archivo: `index.html` (HTML + CSS + JS vanilla, sin build).
- Dependencias por CDN: PeerJS 1.5.4 (WebRTC, conexión teléfono ↔ pantalla, sin servidor propio) y qrcode-generator 1.4.4.
- Vistas: Inicio, Editor, Presentar (host), Jugador (`?join=CODIGO`).
- ID del host en PeerJS: `quiziglesia-<código>`.
- Autoguardado en localStorage + Descargar/Abrir archivo `.quiz.json`.
- Tipos implementados: diapositiva, alternativas, vf, completar, pin, ordenar, numero, encuesta, nube.
- Puntaje: puntos base × multiplicador (normal/doble/sin puntos), bonus por velocidad opcional (hasta −50 %).
- Host: lobby con QR, sacar jugadores, ranking cada N preguntas, podio final, exportar resultados CSV, modo solo pantalla si no hay conexión.
- Jugador: nombre + avatar emoji, reconexión conservando puntaje (pid en localStorage).

## Probado
- Editor y presentación completos, con 5 jugadores simulados (Playwright).
- Pendiente: probar conexión real con teléfonos (PeerJS) una vez publicado.

## Ideas siguientes
Unir parejas, ordenar el versículo, ¿Quién soy? (pistas progresivas), imagen que se revela, clasificar (AT/NT), encontrar el error, emoji-historia, línea de tiempo, modo equipos, escala 1–5; sonidos y música de cuenta regresiva.
