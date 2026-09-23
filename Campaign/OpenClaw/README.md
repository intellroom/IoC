# OpenClaw — suplantación con dropper en shell (zsh)

**TLP:CLEAR**

Cadena de infección de una sola línea: dominio señuelo (`saramoftah[.]com`, con un dominio de staging en `pages.dev`) → comando `curl` con payload **codificado en base64** que decodifica a una segunda descarga vía `curl | zsh`.

**Contenido:** [`Suplantacion.txt`](Suplantacion.txt) — dominios, comando ofuscado con su decodificación, y el inicio del payload.

⚠️ El archivo documenta la técnica de ofuscación (base64 dentro del propio comando) — útil para reglas de detección de `curl | zsh`/`curl | bash` con payload codificado, más allá de los dominios puntuales.
