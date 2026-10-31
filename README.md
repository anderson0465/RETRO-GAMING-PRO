# RETRO GAMING PRO — Android source v0.2

Proyecto Android basado en el emulador.html proporcionado. Se ha mejorado el selector SAF, apertura segura de enlaces externos, manejo del botón Atrás, liberación de WebView y mensajes de motores no disponibles.

## Compilar APK
- Android Studio con JDK 17 y Android SDK 35.
- Abrir esta carpeta, sincronizar Gradle y elegir Build > Build APK(s).
- Alternativamente ejecutar `gradle assembleDebug` con Gradle 8.9 y Android SDK configurados.
- También se incluye `.github/workflows/android.yml` para compilar en GitHub Actions al subir el proyecto a un repositorio propio.

## Estado verificado y limitaciones
- Se ha revisado el código fuente y empaquetado ZIP; **no se ha compilado ni probado una APK en este entorno**.
- NES, SNES, GB, GBA, N64, Genesis, PS1 y Arcade usan el cargador remoto de EmulatorJS: requieren internet y su compatibilidad real no está verificada.
- PSP y PS2 están en la biblioteca pero **NO tienen motores integrados y NO son jugables** en esta versión.
- La importación web guarda archivos en IndexedDB; los archivos muy grandes no son apropiados para esta arquitectura. El límite preventivo de 700 MB no garantiza que el dispositivo tenga cuota suficiente.
- La selección de carpetas depende del WebView del dispositivo.
- No incluye ROMs, BIOS, firmware ni juegos comerciales.

## Para soporte nativo real PSP/PS2
Se necesita integrar y compilar un núcleo Android bajo licencia compatible (PPSSPP para PSP; seleccionar y verificar una implementación legal y mantenida para PS2), acceso SAF a archivos grandes sin copiar a IndexedDB, y pruebas de rendimiento en hardware real. Esto **no está hecho** en v0.2.


## v0.3: Importar carpeta completa
En Android, pulsar **Escanear carpeta** abre el selector nativo ACTION_OPEN_DOCUMENT_TREE. Seleccione una carpeta y conceda permiso. Se recorren subcarpetas hasta 12 niveles y hasta 3000 archivos reconocidos; los archivos se copian a la biblioteca existente sin borrar originales. No se requiere seleccionar uno a uno.

Nota: la implementación usa WebView/IndexedDB y carga cada ROM en memoria para importarla. Para ISOs grandes de PSP/PS2 se requiere posteriormente almacenamiento nativo por streaming; sus motores siguen sin integrarse.
