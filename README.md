🏠 TareasCasa — Guía de instalación y uso
¿Qué es TareasCasa?
Aplicación web progresiva (PWA) para registrar qué tareas del hogar realiza cada hijo, sincronizada con Firebase (Google). Los padres gestionan los datos; los hijos solo pueden ver su progreso en verde/rojo comparado con sus hermanos.
---
📱 Paso 1 — Instalar la app en Android
Opción A: Servir desde un ordenador de casa (red local)
Instala Python si no lo tienes: python.org
Copia la carpeta `tareas-casa/` a tu ordenador
Abre un terminal en esa carpeta y ejecuta:
```
   python3 -m http.server 8080
   ```
En tu Android, abre Chrome y escribe la IP de tu ordenador:
```
   http://192.168.1.X:8080
   ```
(Reemplaza la X con la IP de tu PC — la ves en Configuración → WiFi → Detalles)
Chrome mostrará un banner "Añadir a pantalla de inicio" → Pulsa Instalar
Opción B: Alojar gratis en GitHub Pages (recomendado, acceso desde cualquier lugar)
Crea una cuenta gratuita en github.com
Crea un repositorio nuevo llamado `tareas-casa`
Sube todos los archivos de la carpeta `tareas-casa/`
Ve a Settings → Pages → Source → main → /root → Save
Tu app estará disponible en: `https://TU-USUARIO.github.io/tareas-casa/`
Abre esa URL en Chrome Android → menú (⋮) → Añadir a pantalla de inicio
Opción C: Firebase Hosting (mejor rendimiento)
Instala Node.js y Firebase CLI: `npm install -g firebase-tools`
`firebase login` → `firebase init hosting` → selecciona carpeta `tareas-casa`
`firebase deploy`
Recibes URL tipo `https://tu-proyecto.web.app`
---
🔥 Paso 2 — Configurar Firebase (sincronización entre dispositivos)
Para que los datos se compartan entre el móvil de mamá y el de papá, necesitas Firebase:
Ve a console.firebase.google.com (usa vuestra cuenta Gmail familiar)
Crear proyecto → nombre: `tareas-casa` → Continuar
En el panel: Firestore Database → Crear base de datos → Modo de producción → Elegir región (europe-west1)
Ve a Configuración del proyecto (⚙️) → General → Tu app → clic en el icono web `</>`
Registra la app con nombre `tareas-casa-web`
Copia los valores de `firebaseConfig`:
`apiKey`
`projectId`
`appId`
En TareasCasa: pantalla de login → "Configurar Firebase" → pega los valores → Guardar
Reglas de seguridad Firestore
En Firebase Console → Firestore → Reglas, pega esto:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
(Para uso familiar privado — si quieres más seguridad, contacta a un desarrollador)
---
👨‍👩‍👧 Paso 3 — Configuración inicial de la familia
Entra como Papá / Mamá con el PIN por defecto: `1234`
Ve a ⚙️ Ajustes → Añadir hijo × 3 (uno por cada hijo, con su emoji y color)
Las tareas básicas ya vienen precargadas (poner mesa, quitar mesa, etc.)
Añade las tuyas desde ⚙️ → Nueva tarea o con el botón ＋ en la pestaña Tareas
Cambia el PIN en ⚙️ → Cambiar PIN
---
📖 Uso diario
Como padre/madre:
Abrir la app → Papá / Mamá → introducir PIN
En la pestaña 📋 Tareas, selecciona el hijo que hizo la tarea (pill azul arriba)
Pulsa ＋ junto a la tarea → confirmar → ¡Registrado!
El calendario muestra un punto amarillo los días con actividad; pulsa un día para ver el detalle
El ranking semanal y mensual está en 🏆
Como hijo/a:
Abrir la app → Soy un hijo → seleccionar nombre
Ver sus tareas de la semana con su conteo y el de sus hermanos
Verde = va por delante o igual que sus hermanos
Rojo = va por detrás
No puede registrar ni modificar nada
---
🔒 Seguridad
El PIN de padres se guarda en el dispositivo (y en Firebase si está configurado)
PIN por defecto: 1234 — ¡cámbialo antes de que los hijos lo vean!
Los hijos solo ven datos, nunca pueden modificar nada
---
💾 Backup
En ⚙️ → Exportar datos (JSON) descarga todos los registros
Con Firebase activo, los datos están en la nube automáticamente
---
❓ Preguntas frecuentes
¿Funciona sin internet?  
Sí, los datos se guardan en el dispositivo. Sin Firebase, cada dispositivo tiene sus propios datos. Con Firebase, se sincronizan cuando hay conexión.
¿Puede instalarse en iOS (iPhone)?  
Sí: Safari → botón compartir → "Añadir a pantalla de inicio". Nota: iOS tiene algunas limitaciones con PWAs (sin notificaciones push).
¿Los hijos pueden ver el PIN?  
El PIN solo se pide en el flujo de padres. Los hijos entran directamente seleccionando su perfil.
¿Puedo añadir más de 3 hijos?  
Sí, la app soporta cualquier número de hijos.
---
Versión 1.0 — Generado con TareasCasa
