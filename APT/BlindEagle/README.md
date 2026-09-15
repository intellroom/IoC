# BlindEagle — SVG evasivos y BlotchyQuasar contra el sector asegurador colombiano

**Fecha:** 08-09-2024 · **TLP:CLEAR** · **Fuentes:** VirusTotal Blog, Zscaler

Dos conjuntos de indicadores de BlindEagle (APT-C-36):

1. **`SVG-campaign.txt`** — 16 hashes (MD5/SHA1/SHA256) de archivos SVG no detectados por antivirus, usados como primera etapa de infección. Referencia: [blog de VirusTotal sobre la campaña colombiana](https://blog.virustotal.com/2025/09/uncovering-colombian-malware-campaign.html).
2. **`20240908.md`** / **`20240908_ref.txt`** — indicadores de BlotchyQuasar (hash de muestra + dominios C2 en `linkpc.net`/`publicvm.com`) contra el sector asegurador colombiano. Referencia: [blog de Zscaler](https://www.zscaler.com/blogs/security-research/blindeagle-targets-colombian-insurance-sector-blotchyquasar).
