# 💸 Mi Préstamo

App privada para controlar un préstamo a cuotas fijas: pagos, comprobantes (foto), saldo pendiente, cuotas vencidas y sincronización en tiempo real entre varios teléfonos.

## Seguridad
- **Login obligatorio** (Firebase Authentication, correo + contraseña). Nadie entra sin cuenta.
- **Reglas de Firestore cerradas** con *catch-all* en `false`: solo el dueño y los correos autorizados acceden.
- **Roles**: el **dueño** puede todo; los **miembros** solo ven y registran pagos (no borran ni editan).
- **Código de administrador**: segunda barrera antes de editar/borrar.
- Meta **CSP**, **frame-buster** (anti-clickjacking) y **DOMPurify** para sanear textos.

## Puesta en marcha (una sola vez)
1. Crea un proyecto gratis en https://console.firebase.google.com
2. **Firestore Database** → *Crear base de datos* (modo producción, región europe-west).
3. **Authentication** → *Comenzar* → pestaña *Sign-in method* → activa **Correo electrónico/contraseña**.
4. **Configuración del proyecto (⚙️)** → *Tus apps* → icono web `</>` → registra la app y copia el bloque `firebaseConfig`.
5. Pega ese bloque en `index.html` (donde dice `PEGA_AQUI`).
6. **Firestore → Reglas**: pega el contenido de `FIRESTORE-RULES.txt` y *Publicar*.
7. Abre la web, **crea tu cuenta** (serás el administrador) y configura el préstamo.
8. En *Editar datos → Personas con acceso*, agrega el correo de tu compañero.

Los datos viven en tu Firebase, no dependen del hosting.
