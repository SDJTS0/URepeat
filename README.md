# URepeat MVP 0.1

**Objetivo:** recibir un enlace compartido desde YouTube, abrir un único vídeo en el reproductor oficial y activar el parámetro de repetición (`loop=1` junto con `playlist=VIDEO_ID`).

## Incluye
- Interfaz minimalista, adaptable a móvil.
- Android Web Share Target mediante `manifest.webmanifest`.
- Entrada alternativa por pegar enlace.
- Repetición de una sola pista con el reproductor integrado de YouTube.
- Guarda el ID de la última canción en el almacenamiento local.
- Cancelación de la sesión.
- Service worker básico para caché de la interfaz.

## Límites importantes
- Para aparecer en el menú Compartir de Android, la app debe estar alojada en HTTPS y añadirse/instalarse en el dispositivo como PWA. Abrir `index.html` localmente no registra el destino de compartir.
- La integración de compartir varía según navegador, versión de Android y aplicación de YouTube. Si URepeat no aparece en el menú, copia el enlace y pégalo dentro de URepeat.
- El reproductor oficial puede imponer anuncios, restricciones de reproducción, consentimiento, disponibilidad regional o inicio de sesión.
- El sitio no puede garantizar reproducción en segundo plano ni tomar el control de la app nativa de YouTube. No extrae ni descarga audio.
- En este MVP el título real de la canción no se consulta; se muestra una etiqueta genérica.
- La reproducción automática puede requerir interacción del usuario y depende del navegador.

## Probar localmente
Sirve esta carpeta con un servidor local. Para probar el PWA/share target real, usa HTTPS en un alojamiento estático. No basta con abrir el archivo directamente.

## Despliegue gratuito sugerido
1. Sube estos archivos a un repositorio Git.
2. Activa un alojamiento estático HTTPS (por ejemplo, GitHub Pages).
3. Abre la URL HTTPS en Chrome para Android.
4. Menú ⋮ → **Instalar aplicación** o **Añadir a pantalla de inicio**.
5. Abre YouTube → Compartir en un vídeo → busca URepeat.
6. Si no aparece, usa el campo de enlace como alternativa.

## Estructura
- `index.html`: interfaz, validación de URL y reproductor.
- `manifest.webmanifest`: instalación PWA y destino de compartir.
- `sw.js`: caché de recursos.
- `icon.svg`: icono.

## Git: primer registro
```bash
git init
git add .
git commit -m "feat: create URepeat single-track repeat MVP"
git status
```

## Pruebas manuales
- URL `https://www.youtube.com/watch?v=dQw4w9WgXcQ`: debe extraer un ID de 11 caracteres.
- URL `https://youtu.be/dQw4w9WgXcQ`: debe extraer el mismo ID.
- URL no válida: debe mostrar un aviso y no cargar el reproductor.
- Cancelar: debe retirar el reproductor y borrar la canción guardada.
- Compartir con parámetros `?url=https%3A%2F%2Fyoutu.be%2FdQw4w9WgXcQ`: debe abrir ese vídeo con repetición configurada.
