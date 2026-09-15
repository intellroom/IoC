# Conversores de PDF falsos → ClickFix → Infostealers

**Fecha:** 27-08-2026 · **TLP:CLEAR**
**Fuentes:** FBI Denver, CloudSEK, BleepingComputer, Microsoft, Malwarebytes

Familia de campañas que suplanta servicios legítimos de conversión de PDF (iLovePDF, PDFCandy, Smallpdf y similares). El señuelo funciona porque la víctima **busca activamente** la herramienta — llega por resultados de búsqueda o anuncios, no por correo no solicitado — y el sitio falso **sí entrega el archivo convertido**, por eso nadie sospecha, mientras extrae del documento subido nombres, números de identificación, credenciales bancarias y frases semilla de billeteras cripto.

## Dos mitades que no hay que confundir

1. **Malware** — sitios clonados que entregan infostealers por ClickFix (T1204.004, "pegar y ejecutar") o descarga directa de binario. IOCs públicos y accionables.
2. **Fuga de datos** — el servicio **legítimo** también es un problema, pero de gobernanza de datos, no de malware. No produce IOCs y no se trata como tal (sección 7 de la ficha).

## Línea de tiempo (resumen)

mar-2025 alerta del FBI Denver → 23-03-2025 BleepingComputer confirma dominios reales (`docu-flex[.]com` → Gootloader) → abr-2025 CloudSEK documenta la cadena completa `candyxpdf[.]com` → ClickFix → ArechClient2/SectopRAT → may-2026 Microsoft confirma expansión a macOS → jul-2026 Malwarebytes documenta ClickFix con verificaciones falsas de Google/Cloudflare.

## Documentos

- **[`Conversores_PDF_Falsos_27082026.txt`](Conversores_PDF_Falsos_27082026.txt)** — ficha completa: resumen, línea de tiempo, "lo que NO es un IOC" (los servicios legítimos suplantados), y la sección 7 sobre el riesgo de gobernanza de datos.
- **[`iocs.txt`](iocs.txt)** — indicadores con acción por línea (`BLOQUEAR` / `VIGILAR` / `NO ES IOC` / `DETECTAR`), defanged.
- **[`Conversores_PDF_Falsos_27082026.json`](Conversores_PDF_Falsos_27082026.json)** — misma información en formato estructurado.

## Lo que NO es un IOC (leer antes de bloquear nada)

`ilovepdf[.]com`, `smallpdf[.]com`, `pdfcandy[.]com`, `pdf2go[.]com` son **las víctimas de la suplantación**, no indicadores de compromiso — servicios reales, operativos, con certificación ISO/IEC 27001. Listarlos como IOC es un error de hecho.

---
*Sin diagramas branded en esta campaña (predata la convención de `01_flujo_ataque.png`/`02_modelo_diamante.png`).*
