# MopsStealer: C2 del infostealer en Podaon SIA (Países Bajos)

**Dominio:** `mops[.]to` · **IP:** `45[.]91[.]202[.]47` y `45[.]91[.]202[.]146` (puertos 408 y 1488), más `89[.]105[.]213[.]118` (hallazgo propio) · **Hosting:** Podaon SIA, AS211381, Oude Meer (NL) · **TLP:CLEAR**
**Fecha del análisis:** 27-10-2026 · **Origen:** post de X entregado como texto · **Contrastado:** ThreatFox, MalwareBazaar, Malpedia y fuentes pasivas

**MopsStealer** es una familia nueva de infostealer para Windows: su primera muestra en MalwareBazaar es del 26-09-2026 y su primer indicador en ThreatFox del 18-10-2026. Malpedia la registra **sin descripción ni reglas YARA**, así que casi no hay documentación pública de lo que roba.

Un post de X anuncia **cinco C2 activos** en Podaon SIA: el dominio `mops[.]to` y dos IP, cada una en los puertos **408 y 1488**. Los cinco coinciden uno a uno con ThreatFox, que suma la URL `hxxp://mops[.]to:408/task/Stealer` y tres SHA-256; MalwareBazaar aporta tres muestras (un PowerShell y dos DLL o EXE). En total, **cinco hashes**. Las etiquetas `fake-git` apuntan a **repositorios falsos de software** como vía de entrega: es una etiqueta, no algo verificado aquí.

**Hallazgo propio:** el 28-10-2026 a las 01:17 UTC `mops[.]to` ya no apunta a `45[.]91[.]202[.]47` (como el 21-10 según urlscan) sino a **`89[.]105[.]213[.]118`**, en el mismo sistema autónomo AS211381 y con la misma convención de DNS inverso. No figura en ThreatFox: se publica con confianza media.

Intellroom **no contactó el C2 ni descargó muestras**. No hay víctimas chilenas conocidas: el post y las fuentes no mencionan Chile ni LATAM.

**Por qué el bloqueo lleva fecha:** la infraestructura ya se movió una vez en una semana. El dominio es dedicado y se bloquea entero; las IP son VPS reasignables y se **revisan el 2026-11-27**.

## Correlación

Misma **familia** que otros casos publicados de infostealers con C2 propio: [Phexia_macOS_Polygon_C2](../Phexia_macOS_Polygon_C2) y [Macfinger_ClickFix_macOS](../Macfinger_ClickFix_macOS). Diferencia: MopsStealer es de Windows y, según las etiquetas, llega por repositorios falsos, no por ClickFix. Es correspondencia de tipo de amenaza, no de identidad.

## Evidencia

| | |
|---|---|
| ![Cadena del ataque](01_flujo_ataque.png) | ![Modelo del Diamante](02_modelo_diamante.png) |

![El post, transcrito](03_fuente_post_texto_27102026.png)

| | |
|---|---|
| ![ThreatFox](04_fuente_threatfox_mopsstealer_27102026.png) | ![MalwareBazaar](05_fuente_malwarebazaar_mopsstealer_27102026.png) |

![urlscan, 21-10-2026](06_urlscan_mops_to_408_21102026.png)

## Documentos

- **[`MopsStealer_C2_Podaon_27102026.txt`](MopsStealer_C2_Podaon_27102026.txt)**: ficha completa con resumen, línea de tiempo, lo observado, qué **no** es un IOC, evaluación de la fuente (Admiralty), MITRE ATT&CK verificado, acciones y todo lo que no se pudo verificar.
- **[`iocs.txt`](iocs.txt)**: solo indicadores, con acción por línea (`[BLOQUEAR]` / `[DETECTAR]` / `[VIGILAR]` / `[NO ES UN IOC]`), defanged.
- **[`evidencia_recon_27102026.txt`](evidencia_recon_27102026.txt)** y los RDAP de RIPE (`rdap_ripe_*.json`, recortados a las organizaciones): evidencia con hora UTC. Sumas en **[`evidencia.sha256`](evidencia.sha256)**.

## Lo que no se pudo verificar ni se publica

- **El autor y la fecha del post:** se recibió solo el texto.
- **Qué roba MopsStealer y cómo habla con el C2:** no hay análisis público y no se ejecutó ninguna muestra.
- **El tipo de archivo de dos de los cinco hashes:** solo están en ThreatFox.
- **Si los puertos 408 y 1488 siguen activos** y si `89[.]105[.]213[.]118` sirve hoy el C2: no se contactó.
- **Víctimas y atribución:** ninguna conocida.

---
*Intellroom Threat Intelligence: análisis pasivo. No se contactó el C2 ni se descargó nada del atacante. Las ideas de detección son hipótesis: validar antes de desplegar.*
