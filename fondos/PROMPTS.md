# Fondos 16:9 para las diapositivas

Esta carpeta guarda los fondos que aparecen en la **galería** del editor de diapositivas
(Fondo de la diapositiva → Imagen).

## Cómo agregar fondos

1. Genera las imágenes en **Google Flow** con los prompts de abajo.
2. Descárgalas en la mayor resolución disponible.
3. Pásalas a Claude en el chat. Claude las deja en 1920 × 1080, las comprime, crea una miniatura
   y las agrega a `lista.json`, que es lo que lee la galería.

Formato de cada entrada de `lista.json`:

```json
{ "archivo": "fondo-01.jpg", "mini": "mini/fondo-01.jpg", "nombre": "La creación" }
```

## Cómo usar los prompts en Google Flow

- Crea un proyecto, elige el modo de **imagen** y la relación de aspecto **16:9 (horizontal)**.
- Copia cada prompt tal cual (en inglés suelen dar mejores resultados).
- Todos los prompts ya incluyen el estilo común para que los 20 fondos combinen entre sí y
  con los colores de la app: índigo `#180157`, cian `#06B6D4`, magenta `#A21CAF`, dorado `#F59E0B`.
- Si una imagen sale con letras o caras, vuelve a generarla: los fondos deben dejar espacio
  libre para el título y el texto de la diapositiva.

**Estilo común** (ya va al final de cada prompt):

> soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces

---

## Escenas bíblicas

**01 · La creación**
```
Cosmic scene of the first day of creation: a brilliant beam of golden light breaking through swirling deep indigo darkness, nebulas and soft stars, light spreading like a sunrise over a calm ocean below, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**02 · El jardín del Edén**
```
Lush peaceful garden of Eden at golden hour, gentle river, flowering trees and tall palms, a few friendly animals far in the distance, soft mist and sun rays through leaves, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**03 · El arca y el arcoíris**
```
Large wooden ark resting on a green mountain after the flood, calm reflective water, clouds parting and a soft vivid rainbow across the sky, pairs of small animals walking out in the distance, a white dove flying, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**04 · El mar Rojo abierto**
```
The Red Sea parted into two towering glowing walls of turquoise water with a dry sandy path in the middle leading toward a bright horizon, dramatic but hopeful sky, tiny silhouettes of travelers far away, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**05 · Cielo estrellado del desierto (Abraham)**
```
Vast desert at night under an immense sky full of countless stars and the Milky Way, a few nomad tents glowing warmly at the bottom of the frame, soft dunes, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**06 · Monte Sinaí al amanecer**
```
Majestic rocky mountain at dawn with golden light and soft clouds wrapped around the summit, desert valley below, rays of light descending from the sky, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**07 · Jerusalén antigua al atardecer**
```
Ancient city of Jerusalem on a hill at sunset, stone walls, flat-roofed houses and a grand temple glowing in golden light, olive trees in the foreground, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**08 · Belén y la estrella**
```
Small village of Bethlehem on quiet hills at night, a humble stable with warm lantern light, one bright radiant star shining above, sheep resting on the hillside, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**09 · El mar de Galilea**
```
Calm Sea of Galilee at sunrise, a wooden fishing boat with a folded sail and nets near the shore, gentle hills around the lake, mirror-like water reflecting pink and golden sky, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**10 · El buen pastor (colinas con ovejas)**
```
Green rolling hills with a flock of fluffy sheep grazing, a shepherd's staff leaning against a stone, a small stream, soft morning sunlight and blue sky with light clouds, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**11 · La tumba vacía (Resurrección)**
```
Empty garden tomb carved in rock at sunrise, the large round stone rolled away, brilliant light coming out of the entrance, spring flowers and a path through the garden, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**12 · El sembrador (campo de trigo)**
```
Golden wheat field gently waving in the wind at late afternoon, a winding dirt path, a few birds in the sky and warm sun low on the horizon, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

## Fondos para versículos y momentos especiales

**13 · Pergamino y lámpara (versículos)**
```
Close-up of an old unrolled parchment scroll on a wooden table beside a small glowing oil lamp, soft bokeh background, warm light, the parchment surface mostly blank and soft out of focus, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**14 · Rayos de luz entre las nubes (adoración)**
```
Majestic sky with soft clouds and radiant beams of golden light shining down, heavenly and peaceful atmosphere, gentle gradient from indigo at the top to warm gold near the horizon, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**15 · Noche de oración (cielo con aurora)**
```
Quiet night landscape with a calm lake and distant mountains under a starry sky with a soft flowing aurora in cyan and magenta, peaceful and reflective, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**16 · Ciudad sobre el monte (sal y luz)**
```
A small glowing city on top of a hill at dusk, every window shining with warm light that spreads over the dark valley below, first stars in the sky, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

## Fondos para el juego

**17 · Portada del quiz (abstracto)**
```
Abstract background of smooth flowing waves of deep indigo and magenta light with floating golden sparkles and soft bokeh, modern and festive, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**18 · Ronda de preguntas (abstracto geométrico)**
```
Playful abstract background with soft rounded geometric shapes, circles and rounded squares floating in layers of cyan, indigo and violet with soft shadows and light glow, energetic game show feeling, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**19 · Celebración (ranking y podio)**
```
Joyful celebration background with golden and magenta confetti and streamers falling from the top, soft spotlights and glowing bokeh on a deep indigo backdrop, festive award ceremony feeling, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```

**20 · Despedida (camino al atardecer)**
```
A peaceful path winding through soft hills toward a warm glowing sunset, wildflowers along the path, a few birds flying home, gentle and grateful farewell mood, soft painterly digital illustration for a children's and youth church presentation, warm and hopeful mood, gentle volumetric light, clean uncluttered composition with a large calm empty area in the center for title text, subtle film grain, color palette of deep royal indigo, luminous cyan, soft magenta and warm golden light, 16:9 widescreen, no text, no letters, no words, no logos, no watermarks, no close-up faces
```
