# Fondos 16:9 para las diapositivas

Esta carpeta guarda los fondos que aparecen en la **galería** del editor de diapositivas
(Fondo de la diapositiva → Imagen).

## Cómo agregar fondos

1. Genera las imágenes en **Google Flow** con los prompts de abajo.
2. Descárgalas en la mayor resolución disponible.
3. Pásalas a Claude en el chat (sueltas o en un .zip). Claude las recorta a 16:9 exacto (Flow entrega
   1376 × 768, queda 1365 × 768), las comprime (~100 KB), crea una miniatura de 384 × 216 en `mini/`
   y las agrega a `lista.json`, que es lo que lee la galería.

Los 20 fondos actuales (`fondo-01.jpg` … `fondo-20.jpg`) corresponden a los prompts 01 a 20 de abajo.

> Las imágenes **por historia bíblica** (láminas para contar cada historia) tienen sus propios prompts en
> [`PROMPTS-HISTORIAS.md`](PROMPTS-HISTORIAS.md).

## Clasificación (`lista.json`)

La galería del editor tiene filtros: **Todas · Fondos · Historias**. Con «Fondos» se elige una categoría
y con «Historias» una historia bíblica (agrupadas en Antiguo y Nuevo Testamento; solo aparecen las que
ya tienen imágenes).

Cada imagen tiene un **tipo**:

- `fondo`: imágenes generales para portadas, rondas, celebración, adoración o lugares. Llevan una `categoria`.
- `historia`: escenas de una historia bíblica. Llevan `historias`: una o más historias del catálogo
  (por ejemplo, el mar de Galilea sirve para «Jesús llama a los pescadores» y «Jesús calma la tempestad»).

Un fondo también puede tener `historias` (Jerusalén es un lugar, pero sirve para «La entrada a Jerusalén»):
aparece en los dos filtros.

```json
{ "archivo": "fondo-09.jpg", "mini": "mini/fondo-09.jpg", "nombre": "El mar de Galilea",
  "tipo": "historia", "historias": ["pescadores", "tempestad", "camina-agua"] }
{ "archivo": "fondo-17.jpg", "mini": "mini/fondo-17.jpg", "nombre": "Portada del quiz",
  "tipo": "fondo", "categoria": "portada" }
```

Para agregar una historia o categoría nueva, se suma al catálogo (`historias` o `categoriasFondo`) con un
`id` corto sin espacios.

### Categorías de fondos

| id | Categoría | Imágenes |
|---|---|---|
| `portada` | Portadas y títulos | 1 |
| `preguntas` | Rondas de preguntas | 1 |
| `celebracion` | Celebración y despedida | 2 |
| `adoracion` | Adoración, oración y Palabra | 3 |
| `lugares` | Lugares y paisajes | 1 |

### Historias bíblicas — Antiguo Testamento

| id | Historia | Pasaje | Imágenes |
|---|---|---|---|
| `creacion` | La creación | Génesis 1–2 | 1 |
| `eden` | Adán y Eva en el Edén | Génesis 2–3 | 1 |
| `cain-abel` | Caín y Abel | Génesis 4 | — |
| `noe` | Noé y el arca | Génesis 6–9 | 1 |
| `babel` | La torre de Babel | Génesis 11 | — |
| `abraham` | Abraham y la promesa | Génesis 12–22 | 1 |
| `isaac-jacob` | Isaac, Jacob y Esaú | Génesis 25–33 | — |
| `jose` | José y sus hermanos | Génesis 37–50 | — |
| `moises-bebe` | Moisés en el río | Éxodo 2 | — |
| `zarza` | La zarza ardiente | Éxodo 3–4 | — |
| `plagas` | Las plagas de Egipto | Éxodo 7–12 | — |
| `mar-rojo` | El cruce del mar Rojo | Éxodo 14 | 1 |
| `mana` | El maná en el desierto | Éxodo 16 | — |
| `diez-mandamientos` | Los Diez Mandamientos | Éxodo 19–20 | 1 |
| `jerico` | Josué y los muros de Jericó | Josué 6 | — |
| `gedeon` | Gedeón | Jueces 6–7 | — |
| `sanson` | Sansón | Jueces 13–16 | — |
| `rut` | Rut y Noemí | Rut 1–4 | — |
| `samuel` | El niño Samuel | 1 Samuel 3 | — |
| `david-goliat` | David y Goliat | 1 Samuel 17 | — |
| `david-rey` | David, pastor y rey | 1 Samuel 16; 2 Samuel | 1 |
| `salomon` | Salomón y el templo | 1 Reyes 3–8 | — |
| `elias` | Elías en el monte Carmelo | 1 Reyes 18 | — |
| `naaman` | Naamán y Eliseo | 2 Reyes 5 | — |
| `ester` | La reina Ester | Ester 1–10 | — |
| `nehemias` | Nehemías reconstruye el muro | Nehemías 1–6 | — |
| `horno-fuego` | El horno de fuego | Daniel 3 | — |
| `daniel-leones` | Daniel en el foso de los leones | Daniel 6 | — |
| `jonas` | Jonás y el gran pez | Jonás 1–4 | — |

### Historias bíblicas — Nuevo Testamento

| id | Historia | Pasaje | Imágenes |
|---|---|---|---|
| `anunciacion` | El ángel visita a María | Lucas 1 | — |
| `nacimiento` | El nacimiento de Jesús | Lucas 2 | 1 |
| `pastores` | Los pastores y los ángeles | Lucas 2 | 1 |
| `magos` | Los sabios de Oriente | Mateo 2 | — |
| `nino-templo` | Jesús niño en el templo | Lucas 2 | — |
| `bautismo` | El bautismo de Jesús | Mateo 3 | — |
| `pescadores` | Jesús llama a los pescadores | Lucas 5 | 1 |
| `bodas-cana` | Las bodas de Caná | Juan 2 | — |
| `sermon-monte` | El sermón del monte | Mateo 5–7 | 1 |
| `tempestad` | Jesús calma la tempestad | Marcos 4 | 1 |
| `panes-peces` | Los panes y los peces | Juan 6 | — |
| `camina-agua` | Jesús camina sobre el agua | Mateo 14 | 1 |
| `ciego` | Jesús sana a un ciego | Juan 9; Marcos 10 | — |
| `ninos` | Jesús y los niños | Marcos 10 | — |
| `sembrador` | La parábola del sembrador | Mateo 13 | 1 |
| `oveja-perdida` | El buen pastor y la oveja perdida | Lucas 15; Juan 10 | 1 |
| `hijo-prodigo` | El hijo pródigo | Lucas 15 | — |
| `buen-samaritano` | El buen samaritano | Lucas 10 | — |
| `zaqueo` | Zaqueo | Lucas 19 | — |
| `lazaro` | La resurrección de Lázaro | Juan 11 | — |
| `entrada-jerusalen` | La entrada a Jerusalén | Mateo 21 | 1 |
| `ultima-cena` | La última cena | Lucas 22 | — |
| `getsemani` | Jesús ora en Getsemaní | Mateo 26 | — |
| `cruz` | La cruz | Lucas 23 | — |
| `resurreccion` | La resurrección | Mateo 28; Lucas 24 | 1 |
| `ascension` | La ascensión | Hechos 1 | — |
| `pentecostes` | Pentecostés | Hechos 2 | — |
| `pablo-conversion` | La conversión de Pablo | Hechos 9 | — |
| `pablo-viajes` | Los viajes y el naufragio de Pablo | Hechos 13–28 | — |

### Las 20 imágenes actuales

| Archivo | Nombre | Tipo | Historias |
|---|---|---|---|
| fondo-01.jpg | La creación | Historia | La creación |
| fondo-02.jpg | El jardín del Edén | Historia | Adán y Eva en el Edén |
| fondo-03.jpg | El arca y el arcoíris | Historia | Noé y el arca |
| fondo-04.jpg | El mar Rojo abierto | Historia | El cruce del mar Rojo |
| fondo-05.jpg | Cielo estrellado del desierto | Historia | Abraham y la promesa |
| fondo-06.jpg | Monte Sinaí al amanecer | Historia | Los Diez Mandamientos |
| fondo-07.jpg | Jerusalén antigua | Fondo · Lugares y paisajes | La entrada a Jerusalén |
| fondo-08.jpg | Belén y la estrella | Historia | El nacimiento de Jesús, Los pastores y los ángeles |
| fondo-09.jpg | El mar de Galilea | Historia | Jesús llama a los pescadores, Jesús calma la tempestad, Jesús camina sobre el agua |
| fondo-10.jpg | El buen pastor | Historia | El buen pastor y la oveja perdida, David, pastor y rey |
| fondo-11.jpg | La tumba vacía | Historia | La resurrección |
| fondo-12.jpg | El sembrador | Historia | La parábola del sembrador |
| fondo-13.jpg | Pergamino y lámpara | Fondo · Adoración, oración y Palabra | — |
| fondo-14.jpg | Rayos de luz | Fondo · Adoración, oración y Palabra | — |
| fondo-15.jpg | Noche de oración | Fondo · Adoración, oración y Palabra | — |
| fondo-16.jpg | Ciudad sobre el monte | Historia | El sermón del monte |
| fondo-17.jpg | Portada del quiz | Fondo · Portadas y títulos | — |
| fondo-18.jpg | Ronda de preguntas | Fondo · Rondas de preguntas | — |
| fondo-19.jpg | Celebración | Fondo · Celebración y despedida | — |
| fondo-20.jpg | Despedida | Fondo · Celebración y despedida | — |

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
