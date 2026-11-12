# 📚 Biblioteca del colegio

Catálogo de libros con diseño de consola: libro destacado, estantes horizontales por categoría, búsqueda instantánea y navegación con teclado o control de juegos. Es de código abierto y funciona solo con archivos estáticos.

## Publicar el sitio

1. Sube `index.html`, `books.json` y `README.md` a tu repositorio.
2. En **Settings > Pages** elige la rama `main` y la carpeta `/ (root)`.
3. Tu sitio quedará en `https://TU-USUARIO.github.io/TU-REPOSITORIO/`.

Para probarlo en tu computador no abras el archivo con doble clic. Ejecuta `python3 -m http.server 8000` en la carpeta y entra a `http://localhost:8000`.

## Configuración

Al inicio del `<script>` de `index.html` está el bloque `CONFIG`:

| Campo | Para qué sirve |
|---|---|
| `schoolName` | Nombre que aparece arriba |
| `loanInfo` | Mensaje de cómo pedir un libro |
| `requestUrl` | (Opcional) Enlace a un Google Form para solicitar préstamos |
| `sheetUrl` | (Opcional) Hoja de Google Sheets que todos los visitantes leen en vivo |
| `adminPin` | PIN para abrir el panel de administrador |
| `repoUrl` | Enlace a tu repositorio |

## Importar libros desde Google Sheets

**1. Prepara la hoja.** Primera fila con estos encabezados (solo `titulo` es obligatorio):

`titulo` · `autor` · `categoria` · `isbn` · `año` · `disponible` · `descripcion` · `ubicacion` · `portada` · `color`

En `disponible` escribe Sí / No (o Disponible / Prestado).

**2. Compártela.** En Google Sheets: **Compartir > Acceso general > Cualquier persona con el enlace > Lector**.

**3. Importa.** Pulsa el botón ⚙︎ de la esquina, ingresa el PIN, pega el enlace y elige:
- **Reemplazar catálogo**: la hoja pasa a ser el catálogo completo.
- **Agregar solo libros nuevos**: suma los libros que aún no existen (compara por ISBN o por título y autor).

**4. Publica.** Hay dos caminos:
- **Manual:** pulsa **Descargar books.json** y súbelo al repositorio reemplazando el anterior.
- **En vivo:** pega el enlace de la hoja en `sheetUrl` dentro de `CONFIG`. Desde entonces, todos los visitantes ven los cambios de la hoja al recargar, sin tocar GitHub.

Los cambios hechos en el panel se guardan solo en el navegador de quien los hace (aparece "Vista local" arriba). **Restablecer** vuelve a la versión publicada.

## Portadas reales

Cada libro busca su portada automáticamente al aparecer en pantalla:

1. Por **ISBN** en Google Books.
2. Por **título y autor** en Google Books, verificando que el título coincida.
3. Por ISBN en **Open Library**.

Si no encuentra ninguna, muestra una portada generada con el título, nunca un recuadro en blanco. Los resultados se guardan en el navegador para no repetir la búsqueda.

Para dejar las portadas fijas para todos, abre el panel, pulsa **Buscar portadas** y luego **Descargar books.json**: el archivo incluirá el campo `portada` de cada libro. También puedes poner tu propia imagen en la columna `portada` (enlace o ruta, por ejemplo `covers/libro.jpg`).

Con ISBN la coincidencia es mucho más precisa. Si un libro no tiene ISBN, revisa que la portada sea la correcta.

## Navegación

- **Mouse o toque:** hover con efecto 3D, clic para abrir la ficha.
- **Teclado:** flechas para moverse entre libros, `/` para buscar, `Esc` para cerrar.
- **Control de juegos:** cruceta o palanca izquierda para moverse, `A` para abrir, `B` para cerrar.

## Agregar libros con Pull Request

También puedes editar `books.json` directamente en GitHub (✏️ > Commit changes > Propose changes). Formato de cada libro:

```json
{
  "title": "Título del libro",
  "author": "Nombre del autor",
  "category": "Novela",
  "isbn": "9780000000000",
  "year": 2020,
  "available": true,
  "description": "Una o dos frases sobre de qué trata.",
  "location": "Estante A1",
  "cover": ""
}
```

## Seguridad

El PIN del panel solo oculta las opciones de administración a los alumnos. Como el sitio es estático, cualquiera con conocimientos técnicos puede leerlo en el código. Lo que realmente protege el catálogo publicado es que solo quienes tengan permiso de escritura en el repositorio (o en la hoja de Google) pueden cambiarlo. No guardes datos privados de alumnos en la hoja.

## Licencia

MIT. Agrega un archivo `LICENSE` desde GitHub (**Add file > Create new file**, nombre `LICENSE`, plantilla MIT).
