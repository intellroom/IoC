# Phexia: el stealer de macOS que lee su C2 desde un contrato en Polygon

**Familia:** Phexia, infostealer para macOS en AppleScript · **Entrega:** ClickFix, según fuentes públicas · **Resolución del C2:** contrato inteligente en Polygon (MITRE ATT&CK T1102.001) · **TLP:CLEAR**
**Fuente primaria:** fab0 ([@FABO97662188](https://x.com/FABO97662188)) en X, 27-09-2026 · **Contrastado y ampliado por Intellroom:** 28-09-2026

Phexia no trae escrito el dominio de su servidor de control. El AppleScript le pregunta a un **contrato inteligente en Polygon**, a través de cuatro nodos RPC públicos, cuál es el dominio del momento. Para mover el C2, el operador escribe un valor nuevo con una sola transacción, así que tumbar un dominio no basta: el operador escribe otro y el malware lo lee en su próxima consulta.

fab0 publicó la lista de dominios recientes y una captura del código. Intellroom leyó el contrato directamente en la blockchain, **sin enviar una sola petición a los C2**, y reconstruyó su historia completa. Lo que le da resiliencia al operador también lo expone: cada cambio queda público, firmado y con fecha.

## Lo que esta ficha agrega a lo ya publicado

- **El C2 vigente es `bagueie[.]xyz`**, escrito el **28-09 a las 06:15 UTC**, después del post de fab0. No estaba en su lista.
- **La historia completa del contrato:** desplegado el **1-5-2026**, escrito **31 veces**, con **22 dominios** con forma de C2 y 4 valores de prueba (sitios legítimos). Cada fila lleva el hash de su transacción, para que cualquiera la verifique.
- **La lista de fab0 coincide 1 a 1** con la blockchain, en orden y con sus repetidos: el 22-09 el operador alternó entre `electronic72[.]pro` y `namanami[.]top` tres veces en 34 minutos.
- **La wallet del operador**, `0x363AeAF1F67f1FB7ABdDC3f9806a301f1C64AbE3`, desplegó el contrato y firma cada cambio. Los dominios rotan; la wallet no.
- **Solo 5 de los 22 dominios resuelven hoy.** Tres de los cinco de la lista de fab0 ya están suspendidos por su registro.
- **Cómo leer el C2 vigente sin ejecutar el malware:** una consulta a un nodo público de Polygon (sección 5 de la ficha).

## Indicadores (resumen)

| Tipo | Valor | Acción |
|---|---|---|
| Dominio (C2 vigente) | `bagueie[.]xyz` | Bloquear |
| Dominios (20 anteriores) | Ver `iocs.txt`: 4 aún resuelven | Bloquear; los caídos sirven para buscar en logs desde el 18-05 |
| Dominio | `johncon[.]my` | **Vigilar, no bloquear a ciegas:** puede ser de un tercero |
| Contrato y wallet | `0xA3a603F8…7C15C2A0` · `0x363AeAF1…C64AbE3` | Detectar y vigilar en la blockchain |
| Nodos RPC públicos de Polygon | `polygon.drpc.org` y otros tres | **No bloquear:** son legítimos. Detectar quién los consulta |
| IPs de los C2 | Cloudflare | **No bloquear** la IP ni el rango, solo el dominio |

## Documentos

- **[`Phexia_macOS_Polygon_C2_28092026.txt`](Phexia_macOS_Polygon_C2_28092026.txt)**: ficha completa. Qué agrega a lo publicado, línea de tiempo, indicadores con estado DNS, qué **no** es un IOC, cómo funciona el resolvedor, patrón de rotación, MITRE ATT&CK y todo lo que no se pudo verificar.
- **[`iocs.txt`](iocs.txt)**: solo indicadores, con acción por línea, defanged.
- **[`evidencia_historial_contrato_28092026.txt`](evidencia_historial_contrato_28092026.txt)**: las 31 escrituras del contrato con fecha, valor y hash de transacción.

## Lo que no se pudo verificar ni se publica

- **La atribución a Phexia es de fab0.** Encaja con lo publicado sobre la familia, pero Intellroom no tuvo una muestra.
- **La ruta del C2 después de `check`:** la captura la corta.
- **Que cada dominio histórico haya respondido como C2.** Se afirma que fue el valor del contrato.
- **No hay datos de que la campaña apunte a Chile** ni a un sector en particular.

---
*Intellroom Threat Intelligence: fab0 como fuente primaria; bytecode y estado del contrato leídos con `eth_getCode` y `eth_call` en nodos públicos de Polygon; historial de transacciones en la API de Blockscout; RDAP y DNS de cada dominio; cystack y Cookie Engineer para el contexto de la familia.*
