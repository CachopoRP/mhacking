# CLAUDE_LOG — mhacking

## 2026-08-30 — Fork creado: dependencia real de qbx_crypto que nunca se añadió al proyecto · Claude

**Contexto:** `qbx_crypto` tiene `dependency 'mhacking'` en su `fxmanifest.lua` y dispara eventos reales (`mhacking:show`/`mhacking:start`/`mhacking:hide`, `client/main.lua`) para el minijuego de hackeo al minar cripto. `mhacking` nunca se forkeó a `CachopoRP` ni se añadió al catálogo (`FiveM-Enhanced/config/resources.json`) ni a `server.cfg` — pese a que `qbx_crypto` sí está en `ensure`. Resultado: `qbx_crypto` lleva fallando en cada arranque del server desde que se desplegó (`Failed to load/start resource qbx_crypto. Error: Dependency "mhacking" failed to load. Reason: "Resource "mhacking" not found"`), y el minijuego de cripto nunca ha funcionado en vivo.

**Origen real:** el README de `qbx_crypto` apunta a `qbcore-framework/mhacking`, que ya no existe (repo movido/renombrado). La ubicación actual es **[`Qbox-project/mhacking`](https://github.com/Qbox-project/mhacking)** (mismo patrón que el resto del ecosistema `qbx_*` de este proyecto).

**Copia local en `rpbase` (monolito histórico):** ya existía una copia en `rpbase/mhacking/` — comparada archivo por archivo (`diff`/`cmp`, incluidos los binarios `phone.png` y los `.ogg`) contra `Qbox-project/mhacking` en su `main` actual: **100% idéntica, sin ninguna modificación de CachopoRP**. Confirma que nunca se tocó ni se intentó adaptar — simplemente no se conectó nunca.

**Hecho:**
- Fork `CachopoRP/mhacking` desde `Qbox-project/mhacking` (sin cambios de contenido).
- Rama `cachoporp` creada igual que `main`, siguiendo la convención del resto de recursos.
- Añadido como submódulo en `rpbase-enhanced` (`resources/mhacking`, rama `cachoporp`).
- Recurso simple: solo `client_scripts` + `ui_page` (NUI), sin `server_scripts`, sin natives fuera de lo estándar — no se esperan problemas de compatibilidad Enhanced específicos, pero no se ha probado en vivo el minijuego todavía.

**Pendiente:** registrar en `FiveM-Enhanced/config/resources.json` y añadir `ensure mhacking` a `server.cfg` (antes de `ensure qbx_crypto`, ya que es su dependencia), desplegar, y confirmar en vivo que el minijuego de hackeo abre correctamente al minar cripto.
