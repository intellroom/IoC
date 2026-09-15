# SharePoint on-premise — cadena de RCE no autenticada

**CVE-2026-55040** (CVSS 9.1, bypass JWT) **+ CVE-2026-63520** (CVSS 8.1, RCE vía BCS) · **TLP:CLEAR**
**Fecha:** 27-08-2026 · **Fuentes:** Rapid7, VulnCheck, CISA KEV, Defused, Shadowserver

Cadena pública que lleva de "sin credenciales" a ejecución de código en **Microsoft SharePoint Server on-premise**. Las dos mitades tienen PoC publicado, origen en Pwn2Own Berlin 2026.

> **SharePoint Online / Microsoft 365 NO está afectado. Solo on-premise.**

| CVE | CVSS | Qué es |
|---|---|---|
| CVE-2026-55040 | 9.1 | Bypass de autenticación por forja de token JWT (`SPJsonWebSecurityTokenHandlerV2`). En CISA KEV desde el 18-08-2026. |
| CVE-2026-63520 | 8.1 | Instanciación insegura de tipos .NET en Business Data Connectivity (BCS/BDC) — `Type.GetType()` sobre un nombre de tipo controlado por el atacante. |

## Por qué esta ficha NO trae una blocklist de dominios/IP

Es una **cadena de vulnerabilidad**, no una campaña con infraestructura propia: la acción es **parchear** y **detectar por secuencia**, nunca bloquear. Los endpoints que toca la cadena (`/_api/web/lists`, `/_vti_bin/client.svc/ProcessQuery`) son API legítima de alto uso de SharePoint — bloquearlos rompe el producto.

## Línea de tiempo

14-07-2026 divulgación de CVE-2026-55040 → 11-08-2026 PoC público (Rapid7) → 12-08-2026 weaponización en honeypots, **un día después** → 18-08-2026 CISA agrega a KEV → 24-08-2026 PoC público de CVE-2026-63520 (VulnCheck) → 25-08-2026 encadenamiento observado en honeypots (bypass JWT + enumeración de administradores + sondeo del sink BCS); Defused reporta *"no code execution observed yet"*.

## Documentos

- **[`SharePoint_RCE_Chain_27082026.txt`](SharePoint_RCE_Chain_27082026.txt)** — ficha completa: "lo que NO es un IOC" (los strings literales del PoC, que el atacante cambia con dos palabras), detección por secuencia/contenido, MITRE ATT&CK y acciones.
- **[`iocs.txt`](iocs.txt)** — acción por línea: `[PARCHEAR]` como acción primaria, una sola IP en `[VIGILAR]` (single-source, corroborar antes de accionar), y las señales de detección de alta fidelidad.
- **[`SharePoint_RCE_Chain_27082026.json`](SharePoint_RCE_Chain_27082026.json)** — misma información en formato estructurado.

---
*Sin diagramas branded en esta campaña (predata la convención de `01_flujo_ataque.png`/`02_modelo_diamante.png`) — es una cadena de vulnerabilidad, no una campaña con actor/infraestructura para modelar en el Diamante.*
