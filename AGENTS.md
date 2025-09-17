# Repository Guidelines

## Project Structure & Module Organization
Mantén cada herramienta en su carpeta dedicada con `index.html` y, cuando aplique, `scripts.js` y `styles.css`. Sitúa los recursos compartidos en `img/` y registra licencias adicionales en `licencias/`; agrupa archivos de apoyo por herramienta en `assets/` para evitar rutas rotas. El `index.html` raíz actúa como hub y reutiliza `scripts.js` y `styles.css` globales, así que conserva sus APIs y estilos estables para no romper otras utilidades. Usa siempre rutas relativas al enlazar entre páginas o cargar imágenes.

## Build, Test, and Development Commands
Ejecuta una herramienta concreta con `xdg-open ruta/al/index.html` para validar su comportamiento aislado. Sirve todo el repositorio con `python3 -m http.server 8080` desde la raíz y navega a `http://localhost:8080/` para probar interacciones cruzadas. Para detectar problemas de marcado antes de publicar, lanza `tidy -q -errors index.html` en cada utilidad modificada.

## Coding Style & Naming Conventions
Escribe HTML5 semántico con indentación de 2 espacios y atributos en minúsculas con comillas dobles. Define clases CSS en `kebab-case`, limita los estilos globales y prioriza hojas locales por herramienta. En JavaScript usa `const` y `let`, funciones breves en `camelCase` y evita dependencias externas; documenta cualquier utilidad compartida en `scripts.js` antes de reutilizarla.

## Testing Guidelines
Realiza comprobaciones manuales en Firefox y Chromium, incluyendo viewport móvil con DevTools. Verifica que no existan errores en consola, que los formularios y presets produzcan los resultados esperados y que los `iframe` integrados carguen contenido sin problemas. Comprueba enlaces internos, textos de licencia y comportamiento responsive antes de cerrar la revisión.

## Commit & Pull Request Guidelines
Redacta commits en español siguiendo `tipo(alcance): resumen`, por ejemplo `feat(ui): añadir preset "adoption"`. Limita cada PR a una sola herramienta, explica el motivo del cambio, enlaza issues relevantes y adjunta capturas de `index.html` cuando haya ajustes visuales. Añade una checklist de pruebas (navegadores, responsive, enlaces) y evita introducir nuevas dependencias sin discutirlo.

## Security & Licensing
Respeta `LICENSE.txt` y `LICENSE-CONTENT.txt`; documenta cualquier material nuevo dentro de `licencias/` con su origen. No expongas credenciales ni rutas absolutas, y valida que las fuentes externas cumplan con las licencias del repositorio antes de incorporarlas.
