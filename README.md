# Quiz Iglesia

App web tipo Kahoot para niños y adolescentes de la iglesia: combina diapositivas con rondas de preguntas. Los participantes se unen desde el teléfono con un QR o un código de 5 dígitos.

## Uso

- Abre `index.html` en el navegador (o la versión publicada en GitHub Pages).
- **Editor:** crea el quiz y guárdalo como archivo `.quiz.json` (las imágenes van incluidas).
- **Presentar:** muestra el lobby con QR; los jugadores entran desde su teléfono.
- No necesita base de datos ni servidor propio: la conexión teléfono ↔ pantalla usa PeerJS (WebRTC).

## Tipos de pregunta

Diapositiva, alternativas, verdadero/falso, completar, pin en imagen, ordenar, número, encuesta y nube de palabras.

## Desarrollo

Todo está en un solo archivo `index.html` (HTML + CSS + JavaScript sin compilación). Ver `CLAUDE.md` para el contexto del proyecto.
