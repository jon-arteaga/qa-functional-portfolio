# 🔌 API Checklist — REST Validation

Checklist de validación para pruebas de APIs REST. Para usar durante sesiones exploratorias de API o como sanity check rápido antes de marcar un endpoint como testeado

> 🧠 Ejecutar las requests en **Postman**. Validar los side effects en base de datos con **TablePlus** o **DBeaver**.

---

## 🔐 Autenticación y Autorización

- [ ] Requests sin token devuelven `401 Unauthorized`
- [ ] Requests con token expirado devuelven `401 Unauthorized`
- [ ] Requests con token válido devuelven la respuesta esperada
- [ ] Un usuario no puede acceder a los recursos de otro usuario — devuelve `403 Forbidden`
- [ ] Un rol de menor privilegio no puede ejecutar acciones de admin — devuelve `403 Forbidden`
- [ ] El token malformado es rechazado correctamente (`401`)
- [ ] Las rutas públicas son accesibles sin autenticación

---

## 📋 Request Validation

- [ ] Campos requeridos faltantes devuelven `400 Bad Request`
- [ ] Tipos de datos incorrectos (ej: string en lugar de número) devuelven `400 Bad Request`
- [ ] Body vacío en PATCH/PUT devuelve `400 Bad Request`
- [ ] Campos extra desconocidos en el body son ignorados — no se guardan ni generan error
- [ ] Valores de query params inválidos devuelven `400 Bad Request`
- [ ] El endpoint acepta el `Content-Type: application/json` requerido

---

## 📦 Response Validation

- [ ] Las respuestas exitosas devuelven el status code HTTP correcto `2XX`
- [ ] El response body contiene todos los campos esperados según contrato
- [ ] Los tipos de datos son correctos (string, number, boolean, array, object)
- [ ] Los campos sensibles (password, tokens internos) nunca están expuestos en la respuesta
- [ ] Los timestamps `created_at` y `updated_at` están presentes donde corresponde
- [ ] Los campos de fecha usan formato estándar
- [ ] Las respuestas paginadas incluyen `page`, `limit`, `total` y `total_pages`
- [ ] Listas vacías devuelven `[]`, no `null`

---

## 🔁 CRUD Behavior

- [ ] **POST** crea un nuevo registro — confirmado vía GET después de la creación
- [ ] **PUT** reemplaza todos los campos — payload parcial es rechazado
- [ ] **PATCH** actualiza solo los campos especificados — los demás permanecen sin cambios
- [ ] **DELETE** elimina el recurso — GET devuelve `404` después del borrado
- [ ] Requests POST duplicados devuelven `409 Conflict` donde corresponde

---

## 🧼 Error Handling

- [ ] Recurso inexistente devuelve `404 Not Found`
- [ ] Violaciones de lógica de negocio devuelven `422 Unprocessable Entity`
- [ ] Conflictos (datos duplicados) devuelven `409 Conflict`
- [ ] Las respuestas de error incluyen un mensaje descriptivo — sin stack traces expuestos
- [ ] Los errores de servidor devuelven `500` sin exponer detalles internos

---

## 🗄️ Database Verification

- [ ] Side effects de POST confirmados en DB (registro creado con valores correctos)
- [ ] Side effects de DELETE confirmados en DB (registro eliminado o soft-deleted)
- [ ] PATCH actualiza solo las columnas esperadas — las demás permanecen sin cambios
- [ ] No existen registros duplicados después de requests idénticos repetidos

---

## 📄 Paginación y Filtros (cuando aplica)

- [ ] Los parámetros `page` y `limit` funcionan correctamente
- [ ] Una página fuera del rango devuelve lista vacía, no error
- [ ] Los filtros por campo devuelven resultados correctos y se pueden combinar
- [ ] Los resultados están ordenados según lo esperado

---

## 🔁 Casos Borde

- [ ] IDs con formato inválido (letras en campo numérico) son manejados correctamente
- [ ] Strings con caracteres especiales (`<`, `>`, `"`, `'`) no rompen la respuesta
- [ ] Valores numéricos extremos (0, negativos, muy grandes) son validados
- [ ] El tiempo de respuesta es aceptable
