# Documentos Seguros PWA v0.4 — caja fuerte local cifrada

## Incluye
- PWA con `manifest.json`, icono y service worker para almacenar la interfaz y abrirla sin conexión después de la primera carga.
- Caja fuerte protegida por contraseña.
- Cifrado AES-GCM de 256 bits mediante Web Crypto API; clave derivada con PBKDF2-HMAC-SHA-256 (310,000 iteraciones) y sal aleatoria.
- Registros y archivos adjuntos cifrados juntos antes de guardarse en IndexedDB.
- Búsqueda, categorías, espacios Personal/Familia/Empresa, fecha de vencimiento, notas y adjuntos PDF/imágenes de hasta 15 MB.
- Respaldo `.dsafe` cifrado con una contraseña que se introduce al exportar; restauración con la contraseña del respaldo.

## Cómo probar
1. Extrae el ZIP.
2. Publica la carpeta en un sitio HTTPS o ejecútala desde `localhost`. Abrir el archivo `index.html` directamente no habilita todas las funciones de seguridad/PWA.
3. Abre el sitio en el navegador y crea una contraseña de al menos 10 caracteres.
4. Agrega documentos de prueba y crea un respaldo cifrado `.dsafe`.
5. Cierra y vuelve a abrir para verificar que pide contraseña y conserva los datos.
6. Prueba restaurar el respaldo en una instalación de prueba antes de guardar documentos importantes.

## Instalar
- Android/Chrome: abre el sitio HTTPS y elige “Instalar aplicación” o “Añadir a pantalla de inicio”.
- iPhone/iPad: abre el sitio en Safari, toca Compartir y elige “Añadir a pantalla de inicio”.
- La instalación depende de servir la carpeta en HTTPS; el ZIP no se instala directamente como app.

## Límites importantes
- Esta versión guarda los datos solo en el dispositivo/navegador. No hay nube, cuentas, sincronización entre teléfonos ni pagos.
- La contraseña no se almacena. Si se pierde, los datos cifrados y el respaldo no se pueden recuperar.
- Guarda la contraseña del respaldo por separado. No compartas el archivo `.dsafe` ni la contraseña.
- El service worker almacena los archivos de interfaz para uso offline; la primera visita requiere conexión para cargar la app.
- Es un prototipo, no una auditoría de seguridad. No lo uses todavía como único archivo de documentos críticos. Antes de producción hacen falta pruebas en dispositivos reales, revisión de seguridad, manejo de cuotas/archivos grandes, validación más estricta, CSP y un plan de recuperación.
