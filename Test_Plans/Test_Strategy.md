# 🧪 Test Strategy — E-Commerce Platform

**Proyecto:** Plataforma de e-commerce (B2C)  
**Versión:** 1.0  
**Fecha:** Mayo 2025  
**Autor:** Jonathan Arteaga — QA Analyst

---

## 1. Alcance

### ✅ En scope

- Módulo de autenticación (registro, login, recuperación de contraseña)
- Catálogo de productos (listado, filtros, búsqueda, detalle de producto)
- Carrito de compras (agregar, editar, eliminar ítems)
- Flujo de checkout (datos de envío, métodos de pago, confirmación)
- Historial de pedidos y estado de órdenes
- API REST del backend (endpoints de productos, usuarios y órdenes)
- Validación de datos en base de datos (consistencia de órdenes y stock)

### ❌ Fuera de scope

- Módulo de administración interno (backoffice)
- Integraciones con pasarelas de pago reales (se usan mocks)
- Performance / load testing
- Automatización end-to-end (en roadmap futuro)

---

## 2. Objetivos de Calidad

- Garantizar que los flujos críticos del usuario (registro → compra → confirmación) funcionen sin errores.
- Validar que la API responda con los contratos correctos y manejo de errores adecuado.
- Asegurar la integridad de los datos entre frontend, API y base de datos.
- Detectar regresiones antes de cada release a producción.

---

## 3. Tipos de Testing

| Tipo                    | Descripción                                                          | Herramienta             |
| ----------------------- | -------------------------------------------------------------------- | ----------------------- |
| **Funcional**           | Validación de flujos y reglas de negocio                             | Manual                  |
| **Regresión**           | Re-ejecución de casos críticos ante cambios                          | Manual / TestRail       |
| **Smoke**               | Verificación rápida de funcionalidades base post-deploy              | Manual                  |
| **API Testing**         | Validación de endpoints REST: contratos, status codes, errores       | Postman / Bruno         |
| **Exploratorio**        | Sesiones libres para detectar comportamientos inesperados            | Manual                  |
| **Validación de Datos** | Verificación de integridad y consistencia en DB                      | SQL / DBeaver           |
| **UAT**                 | Validación del flujo completo desde la perspectiva del usuario final | Manual                  |
| **Cross-browser**       | Verificación en diferentes navegadores y resoluciones                | BrowserStack / DevTools |

---

## 4. Prioridades de Testing

Las áreas se priorizan según su impacto en el negocio, la experiencia del usuario y las dependencias técnicas del sistema.

| Prioridad      | Área                      | Razón                                      |
| -------------- | ------------------------- | ------------------------------------------ |
| 🔴 **Crítica** | Checkout y flujo de pago  | Impacto directo en el negocio e ingresos   |
| 🔴 **Crítica** | Autenticación y sesión    | Seguridad y control de acceso              |
| 🟠 **Alta**    | Gestión del carrito       | Parte central del journey del usuario      |
| 🟠 **Alta**    | Endpoints de API          | El frontend depende completamente de ellos |
| 🟡 **Media**   | Catálogo y filtros        | Área de alto tráfico                       |
| 🟡 **Media**   | Comportamiento responsive | Gran base de usuarios mobile               |
| 🟢 **Baja**    | Accesibilidad             | Cumplimiento y usabilidad general          |

---

## 5. Ambientes

| Ambiente        | URL                     | Uso                                 | Base de Datos                  |
| --------------- | ----------------------- | ----------------------------------- | ------------------------------ |
| **Development** | `dev.ecommerce-app`     | Pruebas iniciales del desarrollador | DB dev (datos sintéticos)      |
| **Staging**     | `staging.ecommerce-app` | Validación QA pre-release           | DB staging (copia anonimizada) |
| **Production**  | `www.ecommerce-app.com` | Solo smoke post-deploy              | DB producción (solo lectura)   |

> ⚠️ Las pruebas destructivas (creación/eliminación de datos) se ejecutan únicamente en **staging/QA**.

---

## 6. Herramientas

| Categoría        | Herramienta            |
| ---------------- | ---------------------- |
| Gestión de casos | Xray                   |
| Gestión de bugs  | Jira                   |
| API Testing      | Postman, Bruno         |
| Base de datos    | DBeaver, PostgreSQL    |
| Cross-browser    | BrowserStack, DevTools |
| Documentación    | Confluence, Markdown   |
| Comunicación     | Slack                  |

---

## 7. Recursos y Roles

| Rol               | Responsabilidades                                                     |
| ----------------- | --------------------------------------------------------------------- |
| **QA Analyst**    | Diseño y ejecución de casos, reporte de bugs, validación de APIs y DB |
| **Product Owner** | Definición de criterios de aceptación y priorización                  |
| **Dev Team**      | Desarrollo, revisión y corrección de defectos, soporte en ambientes   |
| **Scrum Master**  | Facilitación del proceso, gestión de impedimentos                     |

---

## 8. Cronograma (Sprint de 2 semanas)

1 sprint = 2 semanas / 10 días laborables

| Actividad                               | Día                |
| --------------------------------------- | ------------------ |
| Kick-off & refinamiento de User Stories | Día 1              |
| Diseño de casos de prueba               | Día 2–3            |
| Ejecución — funcional y API             | Día 4–7            |
| Reporte y seguimiento de bugs           | Día 4–8 (continuo) |
| Regresión y smoke pre-release           | Día 9–10           |
| Sign-off QA                             | Día 10             |

---

## 9. Criterios de Entrada y Salida

### Criterios de Entrada (para comenzar testing)

- User Stories con criterios de aceptación definidos
- Ambiente de staging desplegado y estable
- Datos de prueba disponibles
- Casos de prueba diseñados y revisados

### Criterios de Salida (para aprobar release)

- 100% de casos de smoke ejecutados y aprobados
- 0 bugs críticos o bloqueantes abiertos
- Regresión ejecutada con ≥ 85% de pass rate
- Evidencia de pruebas documentada en TestRail

---

## 10. Gestión de Riesgos

| Riesgo                                    | Probabilidad | Impacto | Mitigación                                                             |
| ----------------------------------------- | ------------ | ------- | ---------------------------------------------------------------------- |
| Ambiente de staging/QA inestable          | Media        | Alto    | Coordinar con el equipo de infra un chequeo previo al ciclo de pruebas |
| Cambios de último momento en el scope     | Alta         | Medio   | Re-priorizar casos críticos y documentar el delta                      |
| Datos de prueba insuficientes o corruptos | Baja         | Alto    | Mantener scripts SQL de seed data actualizados                         |
| Recursos QA limitados (1 analista)        | Media        | Medio   | Priorizar flujos críticos y usar checklists para cobertura rápida      |
| Dependencias de terceros (APIs externas)  | Baja         | Alto    | Usar mocks en staging para aislar el comportamiento                    |

---

## 11. Entregables QA

- [ ] Test Strategy (este documento)
- [ ] Regression Test Plan
- [ ] Suite de casos de prueba en TestRail
- [ ] Reportes de bugs en Jira con evidencia
- [ ] Informe de cierre de ciclo (pass/fail rate, bugs por severidad)
- [ ] Sign-off QA por sprint
