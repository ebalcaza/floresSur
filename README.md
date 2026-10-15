# Flores — galería de naturaleza

Galería de fotografías de flores, plantas y naturaleza en forma de **mosaico**,
hecha con **React + Vite**. Sin títulos ni textos: sólo las imágenes.
Pensada primero para el **celular**, y adaptada a tablets y pantallas grandes.

## Qué tiene

- **Mosaico de distintos tamaños** (normal, ancho, alto, grande) con CSS Grid
  `dense`: el navegador rellena los huecos solo. Las columnas se adaptan al ancho:
  2 en el celular, hasta 6 en pantallas grandes.
- **Visor a pantalla completa** al tocar una imagen:
  - Celular: deslizar ← → para cambiar de foto, deslizar ↓ para cerrar,
    doble toque para hacer zoom.
  - Escritorio: flechas del teclado, `Esc` para cerrar, doble clic para zoom.
  - Muestra primero la miniatura y cambia a la versión grande cuando termina
    de descargarse; precarga la foto anterior y la siguiente.
- **8 temas de color** con degradés pastel y transiciones suaves:

  | Tema | Para qué sirve |
  |---|---|
  | Claro pastel | Buena luz, uso general |
  | Oscuro | De noche |
  | Tierra | Tonos cálidos (marrón / crema) |
  | Bosque | Verdes suaves, descansa la vista |
  | Atardecer | Lavanda y durazno, aire de galería |
  | Penumbra | Ambientes sin luz: muy oscuro, sin luz azul, fotos atenuadas |
  | Alto contraste | Baja visión: negro y amarillo, marcos gruesos, imágenes más grandes |
  | Enfoque suave | Poco enfoque: neutro, sin animaciones, menos imágenes por fila |

- **Control de tamaño** de las imágenes (más chicas / más grandes).
- El tema y el tamaño elegidos **se recuerdan** en el navegador. En la primera
  visita se respeta el modo oscuro o el alto contraste configurados en el sistema.
- **Accesibilidad**: navegación completa con teclado, foco visible, lectores de
  pantalla, botones de 48px o más para el dedo, y se respeta "reducir movimiento".
- **Rendimiento**: miniaturas livianas en WebP generadas por ImageKit, carga diferida
  (`loading="lazy"`) y una conexión al servidor de imágenes abierta de antemano.

## Estructura

```
├── urls-*.csv                 ← lista original de URLs de las imágenes
├── scripts/csv-a-json.mjs     ← convierte el CSV en src/data/imagenes.json
├── src/
│   ├── data/imagenes.json     ← recursos de la galería (generado)
│   ├── temas.js               ← colores de cada tema (único lugar donde se definen)
│   ├── estilos.css            ← cómo se usan esos colores
│   ├── App.jsx                ← componente raíz: tema, tamaño y visor
│   └── components/
│       ├── Galeria.jsx        ← el mosaico (cálculo de columnas)
│       ├── Mosaico.jsx        ← una pieza del mosaico
│       ├── Visor.jsx          ← pantalla completa, gestos y zoom
│       ├── SelectorTema.jsx   ← botón flotante de temas y tamaño
│       └── Iconos.jsx         ← íconos SVG
└── .github/workflows/deploy.yml ← publicación automática en GitHub Pages
```

## Usarlo en tu computadora

Requiere Node.js 20.19 o superior.

```bash
npm install
npm run dev       # servidor de desarrollo en http://localhost:5173
npm run build     # versión final en la carpeta dist/
```

### Cambiar las imágenes

1. Reemplazá el archivo `urls-*.csv` (una URL por línea, con encabezado `url`).
2. Ejecutá `npm run datos` para regenerar `src/data/imagenes.json`.

### Agregar un tema

Agregá un objeto a la lista `TEMAS` en `src/temas.js`. No hace falta tocar el CSS.

## Publicar en GitHub Pages

1. Creá un repositorio en GitHub y subí el código a la rama `main`.
2. En el repositorio: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Cada `push` a `main` publica el sitio automáticamente en
   `https://<tu-usuario>.github.io/<nombre-del-repo>/`.

---

## Ideas para seguir: galería de arte contemporáneo

Propuestas para darle más carácter de galería contemporánea, siempre pensando
primero en el celular:

1. **Modo "sala"**: un recorrido a pantalla completa, una obra por pantalla, con
   deslizamiento vertical tipo *scroll snap* (como historias). Es el formato más
   natural para el pulgar.
2. **Paleta extraída de cada foto**: calcular los 3 colores dominantes de cada imagen
   y usarlos para el degradé del fondo del visor. Cada obra "tiñe" la sala.
3. **Muros temáticos**: agrupar por color (rosas, verdes, ocres) o por hora del día
   (fotos nocturnas vs. diurnas) y filtrar con chips discretos.
4. **Ficha de obra opcional**: tocando un botón "i" en el visor, mostrar fecha y lugar
   (se pueden leer de los datos EXIF o del nombre del archivo, que ya trae la fecha).
5. **Marcos como en un museo**: un tema "Museo" con passe-partout blanco ancho,
   sombra proyectada y fondo de pared gris cálido con textura sutil.
6. **Micro-interacciones de profundidad**: en celulares, inclinar levemente los
   mosaicos con el giroscopio (efecto *parallax*), desactivado en los modos calmos.
7. **Compartir una obra**: que la URL cambie al abrir una foto (`#foto-12`) para poder
   enviar un enlace directo a esa imagen.
8. **Instalable (PWA)**: agregar un *manifest* y un *service worker* para instalarla
   en la pantalla de inicio del celular y verla sin conexión.
9. **Transición compartida**: usar la *View Transitions API* para que la miniatura
   "crezca" hasta la pantalla completa al abrirla.
10. **Curaduría por orden**: permitir reordenar las piezas para crear ritmos visuales
    (una grande, varias chicas, una vertical...) como se montaría una muestra real.
