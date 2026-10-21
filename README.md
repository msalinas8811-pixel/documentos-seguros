# MiVault — PWA v0.17

## Funciones / Features
- Interfaz bilingüe: español e inglés, con selector ES/EN.
- Menú horizontal adaptable a móvil y escritorio.
- Cada opción del menú abre una pantalla independiente dentro de la aplicación; no se desplaza por una página larga.
- Caja fuerte local protegida por contraseña.
- Cifrado AES-GCM de 256 bits y clave derivada con PBKDF2-HMAC-SHA-256 (310,000 iteraciones).
- Registros cifrados con categorías, espacios Personal/Familia/Empresa, vencimiento y notas.
- Adjuntar varios PDF e imágenes a un registro.
- Botón de cámara para capturar fotografías directamente en dispositivos compatibles; permite añadir varias capturas antes de guardar.
- Respaldo `.dsafe` cifrado y restauración protegida por contraseña.
- PWA con manifest, icono y service worker para guardar la interfaz y volver a abrirla sin conexión después de la primera carga.

## Cómo probar / How to test
1. Extrae el ZIP y publica la carpeta en HTTPS o ejecútala desde `localhost`.
2. Abre la app y crea una contraseña de al menos 10 caracteres.
3. Selecciona varios archivos o pulsa “Tomar foto / Take photo” en un dispositivo móvil.
4. Guarda el documento, bloquea la caja fuerte y vuelve a abrirla.
5. Crea un respaldo cifrado y comprueba la restauración.

## Instalación / Installation
- Android: abre el sitio HTTPS en Chrome y elige “Instalar aplicación” o “Añadir a pantalla de inicio”.
- iPhone/iPad: abre el sitio HTTPS en Safari, pulsa Compartir y luego “Añadir a pantalla de inicio”.
- La cámara requiere permiso del navegador y normalmente un contexto HTTPS. El botón de captura puede comportarse distinto según el dispositivo/navegador.
- El ZIP no se instala directamente; primero hay que alojar los archivos en HTTPS.

## Límites de seguridad / Security limitations
- Esta es una versión de prueba, no una auditoría de seguridad.
- Los datos se guardan únicamente en este navegador/dispositivo; no hay nube, cuentas ni sincronización entre teléfonos.
- La contraseña no se almacena. Si se pierde, solo se recupera el acceso con el código de recuperación (desde v0.17). La contraseña de un respaldo `.dsafe` no se puede recuperar.
- Guarda la contraseña del respaldo por separado.
- Usa datos ficticios mientras pruebas. Antes de producción se requieren pruebas en dispositivos reales, auditoría de seguridad, validación adicional de archivos y pruebas de recuperación.


## Navegación por páginas y reportes (v0.8)
- Menú horizontal con acceso a Caja fuerte, Documentos, Reportes y Respaldos.
- Cada opción del menú muestra solo su propia pantalla.
- Registra fecha y hora cuando se pulsa el botón de un archivo adjunto para abrir/descargarlo.
- Filtra el historial por rango de fechas y categoría del documento.
- Exporta los resultados a CSV.
- El historial queda dentro de la bóveda cifrada y es local a este dispositivo; no registra consultas hechas en otros teléfonos.


## Navegación v0.8
Cada opción del menú muestra exclusivamente su pantalla. Las pantallas no seleccionadas se ocultan con `hidden`, `aria-hidden` y reglas CSS explícitas. Al desbloquear la caja fuerte se abre únicamente Caja fuerte. La caché de la PWA se renueva para evitar reutilizar la interfaz anterior.


## MiVault v0.9 — Identidad visual
Nombre de marca actualizado a MiVault en la interfaz y el manifiesto PWA. Se incorporó un icono SVG profesional, el logotipo completo `logo-mivault.png` y una nueva clave de caché para forzar la actualización de recursos. Se conserva el identificador interno de formato de respaldo para mantener la compatibilidad con respaldos cifrados existentes.


## MiVault v0.10 — corrección de reportes por fecha
- El filtro compara fechas del calendario local del dispositivo para evitar desfases por zona horaria.
- Se añadió el botón «Consultar reporte»; los filtros también actualizan el reporte automáticamente.
- La exportación CSV utiliza exactamente los mismos filtros que el reporte en pantalla.


## MiVault v0.11 — actualización del caché
- Cambia la versión del service worker y elimina cachés anteriores al activarse.
- La página principal se solicita primero al servidor para reducir el riesgo de mostrar una versión antigua.
- En Reportes, «Consultar reporte» aplica los filtros; el historial registra aperturas de archivos adjuntos.


## MiVault v0.12 — consulta de documentos por fecha y grupo
- Reportes consulta los documentos guardados, no solo el historial de aperturas de adjuntos.
- Filtros por fecha de creación, grupo (Personal/Familia/Empresa) y tipo de documento.
- Exportación CSV con los mismos filtros.


## MiVault v0.13 — abrir adjuntos desde Reportes
- Añade una columna final con botones para abrir cada archivo adjunto asociado al documento.
- PDF e imágenes intentan abrirse en una pestaña nueva; otros formatos se descargan.
- El botón usa el documento y adjunto almacenados en la caja fuerte local desbloqueada.


## MiVault v0.14 — botón de apertura visible en móvil
- El botón para abrir cada adjunto aparece también debajo del nombre del documento, además de la última columna, para que sea visible en pantallas estrechas.


## MiVault v0.15 — botón único y visor integrado
- Se elimina el botón duplicado; queda uno debajo del nombre del documento, junto al adjunto.
- Fotos e imágenes y PDF se muestran en un visor dentro de MiVault, sin abrir otra página, para evitar perder la sesión desbloqueada al regresar.
- Otros formatos ofrecen descarga desde el visor.


## MiVault v0.16 — botón único en la última columna
- Elimina el botón que aparecía debajo del nombre del documento.
- Conserva únicamente el botón «Abrir archivo» en la columna final de la tabla.
- Mantiene el visor integrado para imágenes y PDF.


## MiVault v0.17 — recuperación de contraseña y mejoras de seguridad

### Cómo funciona la recuperación
- La bóveda ahora se cifra con una **clave maestra aleatoria** (AES-GCM-256). Esa clave se guarda envuelta dos veces: con la contraseña y con un **código de recuperación** de 32 caracteres (160 bits, Base32 Crockford, p. ej. `7KQ2-…`). Ambos envoltorios usan PBKDF2-SHA-256 con 310,000 iteraciones y sal propia.
- Al crear la caja fuerte se muestra el código con opciones para copiar, descargar `.txt` o imprimir. Hay que confirmar que se guardó antes de continuar.
- En la pantalla de desbloqueo, «¿Olvidaste tu contraseña?» permite escribir el código y definir una contraseña nueva **sin perder documentos**. Después se genera un código nuevo y el anterior deja de funcionar.
- Si no se tiene ni contraseña ni código, la única opción es borrar la caja fuerte del dispositivo (hay que escribir BORRAR) y restaurar un respaldo `.dsafe`.
- No hay servidor, correo ni SMS: la recuperación funciona sin conexión y nadie más puede restablecer el acceso.

### Migración automática
- Las cajas fuertes creadas con v0.16 o anteriores (formato 1) siguen abriendo con su contraseña. Al desbloquearlas por primera vez se convierten al formato 2 y se muestra su código de recuperación.
- Los respaldos `.dsafe` mantienen el mismo formato y son compatibles en ambos sentidos.

### Nueva página «Seguridad»
- Cambiar contraseña (requiere la actual; el código de recuperación sigue siendo válido).
- Generar un código de recuperación nuevo (invalida el anterior).
- Bloqueo automático por inactividad: 1, 5 (predeterminado), 15 o 30 minutos, o nunca.

### Otras mejoras
- Límite de intentos: tras 5 contraseñas incorrectas hay una espera creciente (30 s, 60 s… hasta 15 min).
- Medidor de seguridad de contraseña y botón «Ver/Ocultar» en todos los campos de contraseña.
- Panel «Próximos vencimientos» en Caja fuerte y etiquetas «Vencido/Vence pronto» en Documentos.
- Los adjuntos en Documentos se abren en el visor integrado (como en Reportes); el visor tiene botón Descargar y se cierra con Esc.
- Traducción completa al inglés de mensajes, alertas y pantallas que antes quedaban en español; se corrigió la columna «Adjuntos» del reporte.
- Mensajes en línea en lugar de ventanas `alert()`; botones muestran «Procesando…» mientras se cifra.
- Exportación CSV protegida contra inyección de fórmulas en Excel.
- Iconos PNG 192/512 y maskable para instalación en Android/iPhone; logotipo optimizado (de 1.2 MB a ~100 KB).
- Nueva clave de caché del service worker.
