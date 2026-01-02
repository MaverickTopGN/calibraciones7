# Control de PLs — Supabase + Netlify (Static)

## 1) Crear el schema en Supabase
1. Supabase → **SQL Editor** → pega y ejecuta `supabase.sql`.
2. Storage → crea bucket **pl-files** y ponlo **Public** (para poder abrir archivos sin login).

> Si luego quieres seguridad con login, lo dejamos privado y usamos Auth + signed URLs.

## 2) Cargar tu lista (2500)
- Table Editor → tabla **pls** → **Import data** → sube `seed_pls.csv`

## 3) Configurar la web
- Edita `config.js` y pega:
  - `window.__SUPABASE_URL__`
  - `window.__SUPABASE_ANON_KEY__`

## 4) Subir a Netlify
### Recomendado (pro): GitHub + Netlify
- Ventajas: versionado, rollback, deploy automático, trabajo en equipo.
1. Crea repo en GitHub y sube estos archivos.
2. Netlify → **New site from Git** → selecciona repo.
3. Build command: (vacío) / Publish directory: `/` (root)

### Rápido (sin GitHub)
- Netlify → **Deploy manually** → arrastra la carpeta (o ZIP).
- Menos control y sin historial (no recomendado para un proyecto vivo).

## 5) RLS / Policies
Este proyecto viene con RLS habilitado pero con policies abiertas para el rol anon.
Si quieres que solo ustedes lo usen: metemos Auth (magic link) y cerramos policies.


### Si te sale error 'must be owner of table objects'
Usa la UI de Supabase en **Storage → Policies** para el bucket `pl-files`.
Incluí `storage_policies_optional.sql` por si tu proyecto sí permite correrlo por SQL.
