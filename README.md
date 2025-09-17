# Generador de licencias para recursos educativos abiertos (REA)

Herramienta web estática para seleccionar licencias libres recomendadas para contenidos educativos y/o código, y generar materiales listos para documentar un proyecto: prompt para IA, texto plano y bloque HTML con enlaces oficiales. Está pensada para incrustarse como `iframe` (WordPress, LMS, site builder) o para usarse desde el hub de utilidades local.

## Funcionalidades principales
- Presets rápidos (`Reciprocidad`, `Máxima adopción`, `Intermedia`) que combinan licencias Creative Commons y de software libre según el objetivo del proyecto.
- Selector del tipo de recurso (contenidos, código o ambos) que muestra u oculta los grupos de licencias pertinentes.
- Licencias disponibles: contenidos (`CC BY-SA 4.0`, `CC BY 4.0`, `CC BY-NC-SA 4.0`) y código (`AGPL v3`, `MPL 2.0`, `Apache 2.0`, `MIT`), con opción adicional para decidir si la IA enlazará a un `LICENSE.txt` propio o al sitio oficial.
- Campos opcionales de atribución (título, autoría, año, URLs del recurso y de la autoría) para completar el prompt y las salidas generadas.
- Tres formatos de salida sincronizados: prompt de instrucciones para IA, texto plano para README/páginas y bloque HTML accesible con enlaces y metadatos. Cada bloque tiene botón de copiado (`navigator.clipboard`).
- Interfaz multilingüe (es, ca, en, gl, eu) con autodetección del navegador y selector manual, gestionada desde `i18n.js`.
- Persistencia local mediante `localStorage` (`lic-gen:v1`) para recuperar la última configuración, botón de "Borrar datos" para restaurar el estado inicial y ajuste automático de altura del `iframe` mediante `postMessage`.

## Estructura del repositorio
- `index.html`: interfaz principal y punto de entrada para insertar en un `iframe` o abrir en local.
- `scripts.js`: lógica del generador (presets, salidas sincronizadas, copia al portapapeles, persistencia e integración con traducciones).
- `i18n.js`: diccionario de cadenas por idioma y plantillas de texto usadas en las distintas salidas.
- `styles.css`: estilos globales reutilizados por el hub. Incluye diseño responsivo y componentes (tarjetas, botones, campos).
- `img/atribucion.svg`: ilustración usada en la ayuda de atribución.
- `licencias/*.md`: resúmenes en español con enlace al texto oficial de cada licencia usada en la herramienta.
- `LICENSE.txt`: licencia AGPL v3 aplicada al código.
- `LICENSE-CONTENT.txt`: licencia CC BY-SA 4.0 aplicada a los contenidos.

## Cómo probarlo
- Abrir solo esta herramienta: `xdg-open index.html` o arrastrar el archivo al navegador.
- Servir todo el hub localmente: `python3 -m http.server 8080` y visitar `http://localhost:8080/`.
- Validar marcado antes de publicar: `tidy -q -errors index.html`.

### Incrustar en WordPress (u otra web)
1. Publica `index.html`, `scripts.js`, `styles.css`, `i18n.js`, `img/` y `licencias/` bajo la misma carpeta accesible (por ejemplo GitHub Pages).
2. Inserta un bloque "HTML personalizado" y pega:
   ```html
   <iframe
     src="https://tu-dominio.example/utilidades/licencias-libres/index.html"
     style="width:100%;min-height:720px;border:0"
     loading="lazy"
     referrerpolicy="no-referrer"
   ></iframe>
   ```
3. El `iframe` ajusta su altura automáticamente mediante `window.postMessage`. Si tu CMS lo bloquea, define una altura fija (`min-height`) acorde al contenido.

## Flujo dentro de la herramienta
1. Elige el preset o selecciona manualmente licencias para contenidos y/o código.
2. Añade datos de atribución si necesitas que aparezcan en el aviso de licencias.
3. Selecciona el idioma de salida; el contenido del prompt, el texto y el HTML se traducen automáticamente.
4. Copia el formato deseado con los botones "Copiar" y pégalo en README, documentación o página web.

## Personalización
- Añadir nuevas licencias: duplica los `label` y radios pertinentes en `index.html`, amplía los enlaces en `scripts.js` (`LINKS_CC`, `LINKS_CODE`) y documenta el resumen en `licencias/`.
- Modificar presets o estado inicial: edita la constante `PRESETS` y la llamada `setPreset('reciprocity')` al final de `scripts.js`.
- Incluir otro idioma: agrega la traducción completa en `I18N` (`i18n.js`) y enlaza el código ISO en `common.languages`.
- Cambiar estilos: extiende las clases locales en `styles.css`, evitando romper los componentes reutilizados por el hub.

## Licencias y créditos
- Código: GNU AGPL v3 (`LICENSE.txt`).
- Contenidos y documentación: CC BY-SA 4.0 (`LICENSE-CONTENT.txt`).
- Resúmenes de licencias en `licencias/` citan sus fuentes oficiales.
- Autoría original: Juan José de Haro (Bilateria). Reutiliza manteniendo la atribución correspondiente.
