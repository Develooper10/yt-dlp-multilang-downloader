# yt-dlp-multilang-downloader
Herramienta basada en yt-dlp para descargar videos de YouTube con pistas de audio dobladas (ES, JA, KO, EN) en máxima calidad MP4. Permite descargar videos individuales o playlists completas seleccionando el idioma del doblaje oficial. Usa cookies del navegador y motor JS (Deno) para acceder a todos los formatos disponibles.


# YouTube Multi-Language Downloader

Descarga videos de YouTube con pistas de audio dobladas en múltiples idiomas (Español, Japonés, Coreano, etc.) usando `yt-dlp`.

## 📋 Descripción

Herramienta basada en `yt-dlp` que permite:

* Descargar videos con doblajes oficiales en diferentes idiomas.
* Seleccionar la máxima calidad disponible de video y audio.
* Descargar playlists completas con pistas de audio específicas.
* Utilizar cookies del navegador para acceder a contenido restringido.

---

## ⚠️ Cómo YouTube maneja los doblajes

YouTube **no entrega los doblajes como pistas DASH de audio separadas**. Los doblajes suelen aparecer como **streams HLS multiplexados** (video + audio en un único stream).

Por eso:

❌ No funciona:

```bash
-f "bv+ba[language=es]"
```

✅ Sí funciona:

```bash
-f "best*[language=es]"
```

Ejemplos de formatos HLS:

| ID   | Calidad | Idioma  |
| ---- | ------- | ------- |
| 96-3 | 1080p   | Español |
| 95-3 | 720p    | Español |
| 94-3 | 480p    | Español |

---

## 🚀 Requisitos

* Python 3.8 o superior
* FFmpeg
* yt-dlp actualizado
* Deno o Node.js
* Firefox o Chrome

### Instalación

```bash
# Instalar yt-dlp
pip install -U yt-dlp

# Instalar FFmpeg (Windows + Chocolatey)
choco install ffmpeg

# Instalar Deno
irm https://deno.land/install.ps1 | iex

# Reiniciar PowerShell después de instalar Deno
```

---

## 📖 Uso

### Descargar un video en español (máxima calidad)

```powershell
python -m yt_dlp `
  --cookies-from-browser firefox `
  -f "best*[language=es]/best" `
  --merge-output-format mp4 `
  --output "C:\Downloads\%(title)s.%(ext)s" `
  "URL_DEL_VIDEO"
```

### Descargar una playlist completa

```powershell
python -m yt_dlp `
  --cookies-from-browser firefox `
  -f "best*[language=es]/best" `
  --merge-output-format mp4 `
  --output "C:\Downloads\%(playlist_title)s\%(playlist_index)s - %(title)s.%(ext)s" `
  "URL_DE_PLAYLIST"
```

### Descargar usando un ID específico

```powershell
python -m yt_dlp `
  --cookies-from-browser firefox `
  -f "96-3" `
  --output "C:\Downloads\%(title)s.%(ext)s" `
  "URL_DEL_VIDEO"
```

### Mostrar formatos disponibles

```powershell
python -m yt_dlp --cookies-from-browser firefox -F "URL_DEL_VIDEO"
```

---

## 🎯 Parámetros importantes

| Parámetro                        | Descripción                        |
| -------------------------------- | ---------------------------------- |
| `--cookies-from-browser firefox` | Usa las cookies de Firefox         |
| `-f "best*[language=es]"`        | Mejor stream disponible en español |
| `--merge-output-format mp4`      | Convierte el resultado final a MP4 |
| `-F`                             | Lista los formatos disponibles     |
| `-f`                             | Selecciona el formato a descargar  |

---

## 🐛 Solución de problemas

### No aparecen los doblajes al usar `-F`

**Causa:** falta Deno o Node.js.

**Solución:**

```bash
deno --version
```

Si no aparece una versión instalada, instala Deno y reinicia la terminal.

### Descarga en baja calidad

**Causa:**

```bash
bv+ba[language=es]
```

no existe para los doblajes de YouTube.

**Solución:**

```bash
best*[language=es]
```

### Error con los corchetes en PowerShell

Usa comillas simples:

```powershell
-f 'best*[language=es]'
```

---

## 📁 Estructura del proyecto

```text
yt-dlp-multilang-downloader/
├── README.md
├── LICENSE
├── .gitignore
├── Commands
```

---

## 📚 Recursos

* yt-dlp
* FFmpeg
* Deno
* Node.js

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si deseas proponer mejoras importantes, abre primero un issue para discutir los cambios.

---

## 📄 Licencia

Este proyecto está distribuido bajo la licencia MIT. Consulta el archivo `LICENSE` para más información.

---

## ⚖️ Aviso legal

Este proyecto tiene fines educativos. Asegúrate de cumplir con los términos de servicio de YouTube y las leyes de derechos de autor aplicables en tu país.
