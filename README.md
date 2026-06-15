# Grid OS — Android TV Launcher

Launcher nativo para Android TV. Negro/blanco/grises por defecto, totalmente personalizable, perfiles con foto, idioma, modo free-form (arrastrar iconos libres), grid clásico, context menus, animaciones bouncy estilo Material Expressive.

## Compilar el APK desde el teléfono (sin PC)

Recomendado: usar **GitHub Actions** — compila el APK en la nube gratis y lo descargas al teléfono.

### Pasos (10 minutos)

1. Crea cuenta en https://github.com (desde el navegador del teléfono).
2. Crea un repo nuevo, por ejemplo `grid-os`. Marca "Public".
3. Sube el contenido de este ZIP al repo:
   - Opción A (más fácil): En la web de GitHub → `Add file` → `Upload files` → arrastra TODOS los archivos del ZIP (descomprime primero con la app **ZArchiver** o **RAR**).
   - Opción B: Instala la app **GitHub** oficial o **Termux** y haz `git push`.
4. Ve a la pestaña **Actions** del repo. Verás el workflow `Build APK` corriendo automáticamente. Dura ~5 min.
5. Cuando termine (✅ verde), entra al run, baja al final → **Artifacts** → descarga `GridOS-debug-apk.zip`.
6. Descomprime el zip en el teléfono. Adentro está `app-debug.apk`.
7. Pásalo al Android TV con cualquiera de:
   - **Send Files to TV** (app gratis en Play Store, instálala en tele y teléfono).
   - USB / pendrive.
   - Sube a Google Drive y descarga en la TV con un explorador.
8. En la TV, abre el APK con un explorador (ej. **X-plore**) y permite "instalar de fuentes desconocidas".
9. Tras instalar, pulsa el botón **Home** de tu control. Aparecerá un selector — elige **Grid OS** → "Siempre".

### Si el botón Home no muestra el selector

Algunos TVs (especialmente marcas chinas tipo CL / TCL / Coolita) tienen launcher bloqueado. Soluciones:

- Instala **Button Mapper** o **Launcher Manager** desde Play Store y reasigna el botón Home a Grid OS.
- En `Ajustes → Apps → Apps por defecto → App de inicio` (si existe) elige Grid OS.
- En último caso, abre Grid OS desde la lista de apps. Funciona igual aunque no sea el "Home" del sistema.

## Características

- Lista apps TV (Leanback) **y** apps de teléfono sideloadeadas.
- **Perfiles** ilimitados con nombre, foto (desde galería) y tema independiente.
- **Personalización total**: fondo, superficie, texto, acento (HEX), columnas, tamaño de icono, idioma.
- **Free-form**: activa en Ajustes → arrastra iconos donde quieras, posiciones se guardan por perfil.
- **Context menu** (long-press / botón menú): Abrir, Info, Ocultar, Desinstalar.
- **Animaciones bouncy** al enfocar/clic (OvershootInterpolator).
- **Reloj** en cabecera. Botones de Perfil y Ajustes.
- Idiomas: system / EN / ES (más fácil añadir más en `res/values-XX/strings.xml`).

## Estructura
```
app/
 ├─ src/main/AndroidManifest.xml      ← declara HOME + LEANBACK_LAUNCHER
 ├─ src/main/java/com/gridos/launcher/
 │   ├─ ui/MainActivity.kt            ← pantalla principal
 │   ├─ ui/AppAdapter.kt              ← grid bouncy
 │   ├─ ui/SettingsActivity.kt        ← colores, columnas, idioma
 │   ├─ ui/ProfilesActivity.kt        ← gestor de perfiles
 │   ├─ data/AppRepository.kt         ← lista/lanza apps instaladas
 │   ├─ data/Prefs.kt                 ← perfiles + posiciones (JSON en SharedPrefs)
 │   └─ model/AppInfo.kt
 └─ src/main/res/...                  ← layouts, drawables, strings
.github/workflows/build-apk.yml       ← compila el APK en la nube
```

## Notas
- `minSdk 21` (Android 5.0+) — funciona en cualquier Android TV moderno.
- El APK que genera Actions es **debug** (firmado con clave de debug). Suficiente para uso personal. Para Play Store necesitas firmar release.
- Para añadir más idiomas: copia `res/values/strings.xml` a `res/values-fr/strings.xml`, `values-de/`, etc., y traduce.
