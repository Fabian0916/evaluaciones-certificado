# Evaluaciones con certificado

Aplicación estática (sin servidor) para presentar una evaluación de conocimientos y entregar un certificado automático a quien apruebe. Pensada para publicarse en Vercel y guardarse en GitHub.

## Cómo funciona

- **`configurar.html`** — lo usas tú (el administrador). Subes el banco de preguntas (.xlsx o .csv), completas los datos de la evaluación (institución, tema, logo, puntaje mínimo, firma) y descargas un archivo `evaluacion.json`.
- **`evaluacion.json`** — ese archivo descargado reemplaza al que está en esta carpeta. Es la evaluación que verán los participantes. **Cada archivo corresponde a una sola evaluación**: para publicar una nueva, generas otro `evaluacion.json` y lo vuelves a subir.
- **`index.html`** — lo usan los participantes. Carga `evaluacion.json`, pide nombre completo/cargo/fecha, presenta las preguntas, califica (1 punto por respuesta correcta) y, si el puntaje supera el mínimo configurado (90% por defecto), muestra el certificado con botón para imprimir o guardar como PDF.

No hay base de datos ni backend: todo corre en el navegador del participante.

## Formato del archivo de preguntas

Una fila por pregunta, con estas columnas (ver `preguntas_ejemplo.csv`):

| pregunta | opcion_a | opcion_b | opcion_c | opcion_d | respuesta_correcta |
|---|---|---|---|---|---|
| texto de la pregunta | opción 1 | opción 2 | opción 3 | opción 4 | A, B, C o D |

`configurar.html` reconoce variaciones razonables de estos encabezados (por ejemplo "Pregunta", "Opción A", "Respuesta correcta"). Si el archivo tiene menos de 4 opciones, igual funciona con un mínimo de 2.

## Usar en tu computador

1. Abre `configurar.html` haciendo doble clic (no necesitas instalar nada).
2. Sube tu archivo de preguntas, completa los datos y el logo, y descarga `evaluacion.json`.
3. Reemplaza el `evaluacion.json` de esta carpeta por el que acabas de descargar.
4. Abre `index.html` para probar la evaluación como la verá un participante.

## Publicar en GitHub

1. Crea un repositorio nuevo en [github.com](https://github.com) (botón "New repository").
2. En la página del repositorio, usa "uploading an existing file" y arrastra los 5 archivos de esta carpeta (`index.html`, `configurar.html`, `styles.css`, `evaluacion.json`, `preguntas_ejemplo.csv`, `README.md`).
3. Confirma el commit.

Cada vez que generes una nueva evaluación, sube el nuevo `evaluacion.json` desde la misma pantalla de GitHub ("Add file" → "Upload files"), reemplazando el anterior.

## Publicar en Vercel

1. En [vercel.com](https://vercel.com), con tu cuenta ya conectada a GitHub, elige "Add New… → Project".
2. Selecciona el repositorio que acabas de crear.
3. Vercel detecta que es un sitio estático: no necesitas configurar nada, solo dar clic en "Deploy".
4. Obtendrás un enlace público (algo como `tu-proyecto.vercel.app`) que puedes compartir con los participantes — ese enlace siempre muestra la evaluación del `evaluacion.json` más reciente.
5. Para actualizar la evaluación más adelante: sube el nuevo `evaluacion.json` a GitHub y Vercel vuelve a desplegar automáticamente.

## Personalizar colores

Los colores (verde institucional, dorado del certificado) están como variables al inicio de `styles.css`, en `:root`. Cambiar `--brand` y `--gold` ahí actualiza toda la aplicación y el certificado a la vez.
