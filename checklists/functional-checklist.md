# 🧪 Checklist Funcional — Funcionalidades Principales

Checklist de validación funcional para la plataforma de e-commerce. Usar durante sesiones exploratorias, smoke runs o revisiones rápidas de feature readiness antes de la ejecución formal de pruebas.

> 🧠 Usar junto a los casos de prueba para una validación más profunda. Vincular cualquier hallazgo a los bug reports.

---

## 📥 Validación de Inputs

- [ ] Los campos requeridos están marcados visualmente y son validados antes del submit
- [ ] Los mensajes de error inline aparecen para inputs faltantes o inválidos
- [ ] Los campos solo aceptan los caracteres y formatos permitidos (email, teléfono, fecha)
- [ ] Los límites de caracteres están aplicados (ej: nombre, campos de comentario)
- [ ] Los dropdowns y selectores tienen estados por defecto apropiados
- [ ] Los campos con tipo incorrecto (string en lugar de número) son rechazados

---

## 🖱️ Interacción con UI

- [ ] Todos los botones disparan la acción correcta al hacer click
- [ ] Los modales y drawers se abren y cierran correctamente
- [ ] Los botones deshabilitados no pueden ser clickeados y muestran el cursor correcto
- [ ] Los estados de carga aparecen mientras los requests async están en progreso
- [ ] Las notificaciones toast aparecen y se descartan según lo esperado
- [ ] El botón de submit se deshabilita durante el procesamiento para evitar doble envío

---

## 🔐 Autenticación

- [ ] Login con credenciales válidas redirige al destino correcto
- [ ] Login con credenciales inválidas muestra error sin revelar cuál campo es incorrecto
- [ ] El logout devuelve al usuario al home o página de login
- [ ] Las rutas protegidas redirigen al login si no hay sesión activa
- [ ] La sesión expira correctamente y redirige al login con un mensaje informativo
- [ ] La recuperación de contraseña envía el email y el link funciona

---

## 🔄 Flujos de Navegación

- [ ] Todos los links del menú principal llevan a las páginas correctas
- [ ] La navegación hacia atrás preserva el estado anterior (scroll, filtros aplicados)
- [ ] Los redirects después del login llevan al destino correcto
- [ ] Las URLs inválidas devuelven una página `404` amigable
- [ ] Los breadcrumbs reflejan la ubicación actual correctamente (si aplica)

---

## 📋 Comportamiento de Formularios

- [ ] El submit del formulario dispara la acción correcta
- [ ] Los formularios no se envían con campos requeridos faltantes
- [ ] Los formularios multi-step retienen los datos al navegar entre pasos
- [ ] Las acciones de reset o cancelar limpian o descartan los datos correctamente
- [ ] El autofill funciona donde corresponde sin romper el layout
- [ ] Enviar el formulario dos veces no crea registros duplicados

---

## 🛒 Reglas de E-Commerce

- [ ] Los productos se pueden agregar al carrito desde el listado y desde la página de detalle
- [ ] El carrito se actualiza correctamente al cambiar cantidad o eliminar un ítem
- [ ] El flujo de checkout completa end-to-end con datos válidos
- [ ] La orden aparece en el historial inmediatamente después de ser generada
- [ ] Los productos sin stock no se pueden agregar al carrito
- [ ] El total del carrito se recalcula correctamente ante cualquier cambio
- [ ] Aplicar un código de descuento expirado o inválido muestra un error claro

---

## 🔍 Búsqueda y Filtros

- [ ] La búsqueda devuelve resultados relevantes al término ingresado
- [ ] Una búsqueda sin resultados muestra un mensaje claro de "sin resultados"
- [ ] Los filtros aplican correctamente y se pueden combinar
- [ ] Limpiar filtros restaura los resultados completos

---

## 🧼 Error y Manejo de Casos Edge

- [ ] Los fallos de API muestran un error amigable al usuario — sin mensajes técnicos expuestos
- [ ] Los timeouts no dejan la UI en estado de carga indefinido
- [ ] Los errores del servidor (`500`) muestran mensaje amigable, no stack trace
- [ ] Los estados vacíos tienen mensajes descriptivos y/o llamados a la acción

---

## 🧩 Integraciones

- [ ] El proveedor de pago responde correctamente en modo test
- [ ] El email de confirmación de orden se dispara después de la compra
- [ ] El estado del carrito se preserva después de la autenticación
- [ ] Los datos de la orden creada en frontend coinciden con lo registrado en la DB