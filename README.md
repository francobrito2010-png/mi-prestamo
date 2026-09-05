# 💸 Mi Control

App privada para controlar tu dinero con **cuadros**: préstamos (cuotas que terminan) y **gastos mensuales fijos** (alquiler, luz, agua, internet, Netflix, transporte…), con comprobantes (foto), en tiempo real y con funcionamiento offline. Incluye un cuadro **Resumen** con tus totales.

- **Web:** https://francobrito2010-png.github.io/mi-prestamo/
- **Firebase:** proyecto `mi-prestamo-c839b` (Auth correo/contraseña + Firestore).

## Seguridad
- **Login obligatorio** (Firebase Authentication).
- **Reglas de Firestore cerradas** con *catch-all* en `false` (ver `firestore.rules`, se despliega con `firebase deploy --only firestore:rules`).
- **Cada cuadro es privado** de su dueño; se comparte por cuadro añadiendo correos. Los invitados **ven y registran** pagos; **editar/borrar es solo del dueño** (forzado en el servidor).
- **Código de administrador** (por usuario, hash SHA-256) como barrera extra antes de editar/borrar.
- Meta **CSP**, **frame-buster** (anti-clickjacking) y **DOMPurify** para sanear textos.

## Modelo de datos (Firestore)
- `users/{uid}` — perfil privado (guarda `adminHash`).
- `boxes/{boxId}` — un cuadro: `type` (`prestamo`|`gasto`), `ownerUid`, `members[]`, y su configuración.
- `boxes/{boxId}/entries/{id}` — pagos: cuotas (`c1`, `c2`…) o meses (`2026-09`).
- `meta/access`, `loan/*`, `payments/*` — legado del primer préstamo (solo lectura, se migra solo al nuevo formato).
