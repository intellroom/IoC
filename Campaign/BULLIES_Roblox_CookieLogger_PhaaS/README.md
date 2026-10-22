# BULLIES: builder de cookie-loggers de Roblox (phishing-as-a-service) en Vercel

**Plataforma:** "BULLIES" en `werunsyou[.]xyz` · **Objetivo:** cuentas de Roblox (cookie `.ROBLOSECURITY`) · **Hosting:** Vercel (DNS + hosting) · **TLP:CLEAR**
**Fuente:** análisis propio de Intellroom, 2026-10-22. Reconocimiento 100% pasivo (OSINT + lectura del JS del cliente + probe de rutas); nunca se envió una cookie ni se generó una página.

`werunsyou[.]xyz` no es una sola página robacuentas: es una **plataforma de phishing-as-a-service** con marca "BULLIES". Un módulo público, `/generator` ("PAGE GENERATOR"), deja que cualquier operador genere su propia página robacookies de Roblox, que queda viva en el patrón de ruta `/b/[name]`. La cookie de sesión `.ROBLOSECURITY` de la víctima se envía por `POST` a `/api/cookie-logger`, que la reenvía a los webhooks de Discord configurados.

## El modelo de negocio (dual / triple hook)

- **DUALHOOK:** las cookies robadas van al webhook de Discord del operador.
- **TRIPLEHOOK:** agrega un **segundo webhook "reseller"**, es decir la plataforma BULLIES **se queda una copia de cada cookie robada** (skim del operador).
- "Your page goes live instantly at `/b/[name]`"; registra perfil y avatar, saldo de Robux y RAP, ítems raros (Korblox, Headless, Valkyrie), estado de 2FA y correo, e historial de transacciones.
- Comunidad: "BULLIES NETWORK — Access underground modules and real-time logs in our community" (invitaciones de Discord caídas al análisis).

## Infraestructura

| Dato | Valor |
|---|---|
| Dominio | `werunsyou[.]xyz` |
| Creación | 2026-03-09T04:11:57Z |
| Registrar | Name.com, Inc. (IANA 625) · abuse@name.com |
| Estado | clientTransferProhibited |
| DNS / Hosting | Vercel (`ns1/ns2[.]vercel-dns[.]com`; `x-vercel-id iad1`) |
| Stack | Next.js 16.0.10 · React 19.2.0 · pnpm |
| Certificado | Wildcard `*[.]werunsyou[.]xyz` (crt.sh); sin subdominios hermanos |

> No pivotar por IP: Vercel es infraestructura compartida.

## Indicadores

| Tipo | Valor | Acción |
|---|---|---|
| Dominio | `werunsyou[.]xyz` | Bloquear / denunciar |
| URL (exfil) | `hxxps://werunsyou[.]xyz/api/cookie-logger` | Bloquear (POST; GET=405) |
| URL (builder) | `hxxps://werunsyou[.]xyz/generator` | Bloquear |
| Discord | `discord[.]gg/xDQmmHKAxx` | Vigilar (invite expirada, code 50270) |
| Discord | `discord[.]gg/AqXBtrbFvM` | Vigilar (invite caída, code 10006) |

Detalle con acciones por línea: `iocs.txt`.

## Evidencia

Capturas de analista (`01`–`09`) y capturas crudas en texto (`evidencia_*.txt`), con `evidencia.sha256`. Diagramas branded: `01_flujo_ataque.png` (cadena del ataque) y `02_modelo_diamante.png` (Modelo del Diamante).

- `/api/cookie-logger` → HTTP 405 (ruta existe, POST-only), sin enviar datos.
- `/generator` → HTTP 200 (18488 b); `/dashboard`, `/login`, `/panel`, `/admin` → 404.
- WHOIS + crt.sh: ver `09_whois_crtsh.webp` y `evidencia_whois_crtsh_22102026.txt`.
- Discord: ver `evidencia_discord_invites_22102026.txt`.

## Respuesta / baja

- **Vercel (host + DNS):** `vercel.com/abuse` — robo de credenciales, viola su ToS. Vía de baja más rápida (es una fábrica de páginas phishing bajo su hosting).
- **Name.com (registrar):** `abuse@name.com` — suspensión del dominio.

## Método

Observación 100% pasiva: OSINT, lectura estática del JS del cliente, probe de códigos de estado HTTP y consulta a las APIs de WHOIS/crt.sh/Discord. NO se generó ninguna página ni se envió webhook alguno (hacerlo crearía infraestructura maliciosa viva), y nunca se ingresó una cookie en el panel. Víctimas: usuarios de Roblox (categoría genérica, sin datos personales).
