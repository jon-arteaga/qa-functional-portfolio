# 🔁 Regression Test Plan — E-Commerce Platform

**Proyecto:** Plataforma de e-commerce (B2C)  
**Versión:** 1.0  
**Fecha:** Mayo 2025  
**Autor:** Jonathan Arteaga — QA Analyst  
**Tipo de regresión:** Pre-produción

---

## 1. Objetivo

Garantizar que los cambios introducidos en cada sprint no rompan funcionalidades existentes. La regresión se ejecuta sobre los flujos críticos del sistema antes de cada release a producción

---

## 2. Alcance de la Regresión

### ✅ Flujos críticos incluidos

| #   | Módulo        | Flujo                                              |
| --- | ------------- | -------------------------------------------------- |
| 1   | Autenticación | Registro de nuevo usuario                          |
| 2   | Autenticación | Login con credenciales válidas                     |
| 3   | Autenticación | Login con credenciales inválidas (manejo de error) |
| 4   | Catálogo      | Búsqueda de producto por nombre                    |
| 5   | Catálogo      | Filtrado por categoría y precio                    |
| 6   | Carrito       | Agregar producto al carrito                        |
| 7   | Carrito       | Modificar cantidad de un ítem                      |
| 8   | Carrito       | Eliminar ítem del carrito                          |
| 9   | Checkout      | Completar compra con tarjeta (mock)                |
| 10  | Checkout      | Validación de campos obligatorios en formulario    |
| 11  | Órdenes       | Visualización del historial de pedidos             |
| 12  | Órdenes       | Verificación de estado de orden en DB              |
| 13  | API           | `GET /products` — listado con paginación           |
| 14  | API           | `POST /orders` — creación de orden                 |
| 15  | API           | `GET /users/{id}` — datos de usuario autenticado   |

### ❌ Excluido de la regresión

- Módulo de administración (backoffice)
- Funcionalidades nuevas del sprint actual (cubiertas por pruebas funcionales)
- Tests de performance

---

## 3. Criterios de Entrada

Antes de iniciar la ejecución de regresión se deben cumplir:

- [ ] Build desplegado en staging sin errores de compilación
- [ ] Smoke test inicial aprobado (funcionalidades base operativas)
- [ ] Suite de regresión actualizada con los cambios del sprint
- [ ] Datos de prueba disponibles y validados en el ambiente

---

## 4. Criterios de Salida

La regresión se considera aprobada cuando:

- [ ] 100% de los casos de la suite ejecutados
- [ ] Pass rate ≥ 90%
- [ ] Los casos fallidos no deben afectar flujos críticos de negocio
- [ ] 0 bugs con severidad **Crítica** o **Alta** abiertos
- [ ] Bugs de severidad **Media** o **Baja** documentados en Jira con ticket asignado
- [ ] Evidencia de ejecución registrada en XRay

---

## 5. Suite de Regresión

### Módulo: Autenticación

| ID          | Caso de Prueba                         | Prioridad | Resultado Esperado                      |
| ----------- | -------------------------------------- | --------- | --------------------------------------- |
| REG-AUTH-01 | Registro exitoso con datos válidos     | Alta      | Usuario creado, redirige al dashboard   |
| REG-AUTH-02 | Login con email y contraseña correctos | Alta      | Sesión iniciada, token generado         |
| REG-AUTH-03 | Login con contraseña incorrecta        | Alta      | Error 401, mensaje de error visible     |
| REG-AUTH-04 | Registro con email ya existente        | Media     | Error informativo, no se crea duplicado |

### Módulo: Catálogo

| ID         | Caso de Prueba                                     | Prioridad | Resultado Esperado                          |
| ---------- | -------------------------------------------------- | --------- | ------------------------------------------- |
| REG-CAT-01 | Búsqueda por nombre devuelve resultados relevantes | Alta      | Lista filtrada correctamente                |
| REG-CAT-02 | Filtro por categoría funciona correctamente        | Alta      | Solo se muestran productos de esa categoría |
| REG-CAT-03 | Filtro por rango de precio aplica correctamente    | Media     | Productos dentro del rango mostrados        |
| REG-CAT-04 | Detalle de producto muestra información completa   | Alta      | Nombre, precio, stock, imágenes presentes   |

### Módulo: Carrito

| ID          | Caso de Prueba                                        | Prioridad | Resultado Esperado                         |
| ----------- | ----------------------------------------------------- | --------- | ------------------------------------------ |
| REG-CART-01 | Agregar producto al carrito                           | Alta      | Ítem aparece en carrito con cantidad 1     |
| REG-CART-02 | Aumentar cantidad de un ítem                          | Alta      | Cantidad actualizada, subtotal recalculado |
| REG-CART-03 | Eliminar ítem del carrito                             | Alta      | Ítem removido, total actualizado           |
| REG-CART-04 | Carrito persiste al cerrar sesión y volver a ingresar | Media     | Ítems mantienen el estado                  |

### Módulo: Checkout

| ID         | Caso de Prueba                                      | Prioridad | Resultado Esperado                                |
| ---------- | --------------------------------------------------- | --------- | ------------------------------------------------- |
| REG-CHK-01 | Completar compra con datos válidos                  | Alta      | Orden creada, confirmación visible, email enviado |
| REG-CHK-02 | Intentar checkout sin completar campos obligatorios | Alta      | Mensajes de validación visibles, no avanza        |
| REG-CHK-03 | Verificar total calculado correctamente en resumen  | Alta      | Total = suma de ítems + envío                     |

### Módulo: API

| ID         | Endpoint         | Método | Validación                                           | Prioridad |
| ---------- | ---------------- | ------ | ---------------------------------------------------- | --------- |
| REG-API-01 | `/products`      | GET    | Status 200, array de productos con campos requeridos | Alta      |
| REG-API-02 | `/orders`        | POST   | Status 201, orden creada con ID en respuesta         | Alta      |
| REG-API-03 | `/users/{id}`    | GET    | Status 200 con token válido / 401 sin token          | Alta      |
| REG-API-04 | `/products/{id}` | GET    | Status 404 para ID inexistente                       | Media     |

---

## 6. Gestión de Defectos

Los bugs encontrados durante la regresión se reportan en **Jira** con la siguiente clasificación:

| Severidad      | Descripción                                          | Acción                                      |
| -------------- | ---------------------------------------------------- | ------------------------------------------- |
| 🔴 **Crítica** | El sistema no funciona, flujo bloqueado              | Bloquea el release. Fix inmediato requerido |
| 🟠 **Alta**    | Funcionalidad importante rota con workaround difícil | Bloquea el release si no hay fix            |
| 🟡 **Media**   | Bug visible pero con workaround disponible           | Documentar, puede ir al siguiente sprint    |
| 🟢 **Baja**    | Problema estético o de UX menor                      | Backlog, no bloquea                         |

---

## 7. Reporte de Regresión

Al cierre de cada ciclo de regresión, se comparte un resumen con el equipo:

```
Sprint: [Número de sprint]
Fecha: [Fecha]
Ambiente: [Donde se hizo la regresión]

Total TCs ejecutados: X
  ✅ Pass: X
  ❌ Fail: X
  ⚠️ Bloqueados: X

Bugs críticos encontrados: X
Bugs de alta severidad encontrados: X

Recomendación de release: ✅ GO / ❌ NO-GO
Notas: [Observaciones relevantes]
```
