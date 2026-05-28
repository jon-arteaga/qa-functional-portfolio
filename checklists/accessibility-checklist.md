# ♿ Accessibility Checklist — WCAG 2.1 AA

Checklist de validación de accesibilidad basada en los criterios de WCAG 2.1 nivel AA. Orientada a verificar que la aplicación sea usable para personas con distintas capacidades. 

> 💡 Esta checklist es una guía de revisión manual básica. Para auditorías completas se recomienda complementar con herramientas como Axe, Lighthouse o NVDA

---

## ⌨️ Navegación por Teclado

- [ ] Todos los elementos interactivos son alcanzables con la tecla `Tab`
- [ ] El orden de foco sigue una secuencia lógica (de arriba a abajo, izquierda a derecha)
- [ ] El indicador de foco es siempre visible — ningún elemento pierde el focus ring
- [ ] Los formularios se pueden completar y enviar usando solo el teclado
- [ ] Los modales atrapan el foco mientras están abiertos y lo devuelven al cerrarse
- [ ] La tecla `Escape` cierra modales, dropdowns y drawers
- [ ] No hay trampas de teclado (el usuario puede salir de cualquier componente)

---

## 🔊 Lector de Pantalla

- [ ] Todas las imágenes tienen texto `alt` descriptivo — no vacío ni genérico ("image", "foto")
- [ ] Las imágenes decorativas tienen `alt=""` para ser ignoradas por lectores de pantalla
- [ ] Todos los campos de formulario tienen `<label>` asociado o `aria-label`
- [ ] Los mensajes de error son anunciados después del submit del formulario
- [ ] La página tiene un `<title>` con contenido descriptivo y significativo
- [ ] Los encabezados siguen una jerarquía lógica (H1 → H2 → H3)
- [ ] Los botones con solo íconos tienen un label accesible (`aria-label`)
- [ ] Los landmarks de página están definidos (`<main>`, `<nav>`, `<header>`, `<footer>`)

---

## 🎨 Color y Contraste

- [ ] El contraste del texto normal cumple ratio mínimo de **4.5:1**
- [ ] El texto grande (≥ 18px o 14px bold) cumple ratio mínimo de **3:1**
- [ ] Los elementos interactivos (botones, links) cumplen los requisitos de contraste
- [ ] La información no se transmite únicamente por color — siempre incluye label, ícono o patrón
- [ ] Los estados de foco tienen contraste suficiente contra el fondo

---

## 📱 Accesibilidad Mobile

- [ ] Los elementos táctiles tienen al menos **44×44 CSS px**
- [ ] Los elementos no están demasiado juntos — los taps accidentales son poco probables
- [ ] El zoom de pellizco no está deshabilitado (`user-scalable=no` no está en uso)
- [ ] El contenido es legible sin scroll horizontal en **320px de ancho**

---

## 🧩 Estructura Semántica

- [ ] La página usa elementos HTML semánticos (`<nav>`, `<main>`, `<footer>`, `<button>`)
- [ ] Los links tienen texto descriptivo — no "click aquí" o "leer más" solos
- [ ] Las tablas tienen `<th>` correctamente definidos si son usadas
- [ ] Las listas usan `<ul>` o `<ol>` — no `<div>` estilizados como lista

---

## 🎬 Multimedia y Movimiento

- [ ] Los videos tienen subtítulos o transcripciones disponibles
- [ ] No hay contenido que destelle más de 3 veces por segundo (riesgo de convulsiones)
- [ ] Las animaciones que se reproducen automáticamente tienen opción de pausa