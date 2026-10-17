# Documentos Seguros / Secure Documents — PWA v0.7

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
- La contraseña no se almacena. Si se pierde, no se puede recuperar la caja fuerte ni el respaldo.
- Guarda la contraseña del respaldo por separado.
- Usa datos ficticios mientras pruebas. Antes de producción se requieren pruebas en dispositivos reales, auditoría de seguridad, validación adicional de archivos y pruebas de recuperación.


## Navegación por páginas y reportes (v0.7)
- Menú horizontal con acceso a Caja fuerte, Documentos, Reportes y Respaldos.
- Cada opción del menú muestra solo su propia pantalla.
- Registra fecha y hora cuando se pulsa el botón de un archivo adjunto para abrir/descargarlo.
- Filtra el historial por rango de fechas y categoría del documento.
- Exporta los resultados a CSV.
- El historial queda dentro de la bóveda cifrada y es local a este dispositivo; no registra consultas hechas en otros teléfonos.
