# 🗂️ Test Plans

Documentos de estrategia y planificación de QA para una plataforma de e-commerce. Estos artefactos reflejan prácticas reales de planificación utilizadas en entornos Agile/Scrum.

---

## ¿Qué es un Test Plan?

El Test Plan es el documento de **más alto nivel** dentro del proceso QA. Antes de ejecutar una sola prueba, el equipo necesita tener claro el mapa del proyecto: qué se va a testear, cómo, con qué recursos y bajo qué condiciones.

Un Test Plan bien definido responde a estas preguntas clave:

| Sección              | ¿Qué define?                                                           |
| -------------------- | ---------------------------------------------------------------------- |
| **Alcance**          | Qué funcionalidades entran y cuáles quedan fuera del testing           |
| **Estrategia**       | Cómo se va a abordar la calidad: tipos de prueba, niveles, prioridades |
| **Tipos de testing** | Funcional, regresión, smoke, exploratorio, API, UAT, etc.              |
| **Recursos**         | Equipo involucrado, roles y responsabilidades                          |
| **Ambientes**        | Dev, staging, producción — configuraciones y datos de prueba           |
| **Cronograma**       | Estimaciones, hitos y fechas de entrega                                |
| **Riesgos**          | Qué puede salir mal y cómo se mitiga                                   |

> Es básicamente el **mapa del proyecto** QA. Sin él, el equipo trabaja sin dirección clara y la cobertura queda al azar.

---

## 📁 Estructura

```
Test_Plans/
├── Test_Strategy.md          # Estrategia QA general: alcance, tipos de prueba, ambientes y entregables
└── Regression_Test_Plan.md   # Plan de regresión: flujos críticos, criterios de entrada/salida y suite de pruebas
```

---

## 📂 Explorar

| Archivo                   | Descripción                                                                              |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| `Test_Strategy.md`        | Estrategia QA completa: alcance, tipos de testing, ambientes, herramientas y entregables |
| `Regression_Test_Plan.md` | Plan de regresión con flujos críticos, criterios de entrada/salida y suite de pruebas    |

---

🔒 _Todo el contenido es generalizado y fue creado con fines de portfolio. Cualquier similitud con productos o empresas reales es coincidencia. Los nombres de clientes y proyectos fueron omitidos para respetar la confidencialidad._
