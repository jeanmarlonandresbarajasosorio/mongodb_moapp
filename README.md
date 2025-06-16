# 🏦 Proyecto: Banco Digital - Taller de Expresiones Regulares con MongoDB

## 📌 Descripción del sistema

**Banco Digital** es un sistema de gestión bancaria diseñado para simular las operaciones básicas de una entidad financiera. La base de datos incluye información de clientes, cuentas bancarias, transacciones realizadas, empleados de distintas sucursales y solicitudes de crédito. Este proyecto permite realizar consultas útiles a través de expresiones regulares, facilitando análisis, filtros y búsquedas eficientes.

---

## 🧱️ Estructura de la base de datos

La base de datos contiene **5 colecciones principales**, cada una con al menos 15 documentos realistas:

| Colección             | Descripción                                                                  |
| --------------------- | ---------------------------------------------------------------------------- |
| `clientes`            | Información personal de los clientes (nombre, correo, ciudad, profesión...)  |
| `cuentas`             | Datos sobre cuentas bancarias activas, tipo y saldo                          |
| `transacciones`       | Historial de movimientos entre cuentas (origen, destino, monto, descripción) |
| `empleados`           | Datos del personal bancario, su cargo, sucursal y horario de trabajo         |
| `solicitudes_credito` | Registros de solicitudes de préstamo, su estado y comentarios del análisis   |

---

## ⚙️ ¿Cómo crear la base de datos en MongoDB?

1. Abre tu terminal y ejecuta `mongosh` para iniciar el shell de MongoDB.
2. Crea la base de datos:

   ```js
   use bancoDigital
   ```
3. Importa los archivos `.json` de cada colección usando el siguiente formato:

```bash
mongoimport --db bancoDigital --collection clientes --file clientes.json --jsonArray
mongoimport --db bancoDigital --collection cuentas --file cuentas.json --jsonArray
mongoimport --db bancoDigital --collection transacciones --file transacciones.json --jsonArray
mongoimport --db bancoDigital --collection empleados --file empleados.json --jsonArray
mongoimport --db bancoDigital --collection solicitudes_credito --file solicitudes_credito.json --jsonArray
```

>  Asegúrate de ejecutar los comandos desde la misma carpeta donde están ubicados los archivos `.json`.

---

## 🗂️ En la carpeta Archivos.json incluye 

| Archivo                    | Colección en MongoDB  |
| -------------------------- | --------------------- |
| `clientes.json`            | `clientes`            |
| `cuentas.json`             | `cuentas`             |
| `transacciones.json`       | `transacciones`       |
| `empleados.json`           | `empleados`           |
| `solicitudes_credito.json` | `solicitudes_credito` |

---

## 🔍 Consultas con Expresiones Regulares (25)

Incluyen una explicación breve sobre su utilidad en el sistema:
---

### Consulta 1: Buscar clientes cuyo nombre comience por "Juan" (autocompletar en buscador)

```js
db.clientes.find({ nombre: { $regex: "^Juan" } })
```

Esta consulta se usa para autocompletar campos en formularios de búsqueda cuando el usuario empieza a escribir nombres como "Juan Carlos", "Juanita", etc.

### Consulta 2: Clientes con correos de hotmail (segmentación de marketing)

```js
db.clientes.find({ correo: { $regex: "@hotmail\\.com$", $options: "i" } })
```

Permite identificar clientes que usan correos de hotmail para enviar promociones personalizadas o realizar campañas segmentadas.

### Consulta 3: Clientes que viven en ciudades que terminan en "a" (estadísticas por región)

```js
db.clientes.find({ ciudad: { $regex: "a$" } })
```

Filtra clientes que viven en ciudades como "Bogotá", "Cartagena" o "Barranquilla" para analizar regiones más activas.

### Consulta 4: Clientes cuyo nombre tenga la palabra "Juan" (filtrado rápido de usuarios)

```js
db.clientes.find({ nombre: { $regex: "Juan", $options: "i" } })
```

Busca clientes con nombre o apellido "Juan" para atención personalizada en soporte.

### Consulta 5: Buscar por profesión que incluya la palabra "teacher" (ofertas segmentadas)

```js
db.clientes.find({ profesion: { $regex: "teacher", $options: "i" } })
```

Filtra clientes con profesiones afines para ofrecer créditos especializados o productos financieros.

### Consulta 6: Buscar transacciones cuya descripción comience con "Pago"

```js
db.transacciones.find({ descripcion: { $regex: "^Pago", $options: "i" } })
```

Filtra movimientos relacionados con pagos recurrentes, útiles para generar reportes mensuales.

### Consulta 7: Transacciones con descripción que contiene "compra"

```js
db.transacciones.find({ descripcion: { $regex: "compra", $options: "i" } })
```

Permite identificar todas las compras realizadas desde las cuentas del banco, útil para análisis de consumo.

### Consulta 8: Buscar cuentas cuyo tipo comience por "corr"

```js
db.cuentas.find({ tipo: { $regex: "^corr", $options: "i" } })
```

Útil para obtener rápidamente todas las cuentas corrientes activas.

###  Consulta 9: Solicitudes de crédito con comentarios que incluyan la palabra "alto"

```js
db.solicitudes_credito.find({ comentarios: { $regex: "alto", $options: "i" } })
```

Detecta solicitudes con advertencias sobre el perfil del cliente, útil para análisis de crédito.

### Consulta 10: Empleados cuyo nombre termina en "ez"

```js
db.empleados.find({ nombre: { $regex: "ez$", $options: "i" } })
```

Filtra empleados con apellidos comunes como "Martínez", "Gómez", etc., para efectos administrativos.

### Consulta 11: Empleados con correo (terminado en @hotmail.com)

```js
db.empleados.find({correo: {$regex:"@hotmail\\.com$"
}})
```

Permite verificar qué empleados usan correo hotmail.com.

###  Consulta 12: Clientes con ciudad que incluya "Balea"

```js
db.clientes.find({ ciudad: { $regex: "Balea", $options: "i" } })
```

Filtra clientes de Baleares y variantes como "Baleares Norte", "Zona Baleares", etc.

### Consulta 13: Empleados cuyo cargo contiene "gerente"

```js
db.empleados.find({ cargo: { $regex: "gerente", $options: "i" } })
```

Útil para extraer personal con cargos directivos o de supervisión.

### Consulta 14: Solicitudes de crédito con estado "aprob"

```js
db.solicitudes_credito.find({ estado: { $regex: "aprob", $options: "i" } })
```

Muestra rápidamente todas las solicitudes aprobadas, en cualquier estado de proceso.

###  Consulta 15: Clientes cuyo nombre tenga tres palabras (nombres y apellido)

```js
db.clientes.find({ nombre: { $regex: "^\\w+\\s\\w+\\s\\w+$" } })
```

Filtra registros con formato de nombre completo estándar, útil para validar datos.

### Consulta 16: Transacciones con descripciones que contengan números

```js
db.transacciones.find({ descripcion: { $regex: "\\d+" } })
```

Permite detectar descripciones con números (facturas, códigos, etc.).

### Consulta 17: Empleados con turnos en horario nocturno

```js
db.empleados.find({ turno: { $regex: "Noche" } })
```

Identifica personal que trabaja en turno nocturno para asignaciones especiales.

### Consulta 18: Clientes con correos que no sean de dominios populares

```js
db.clientes.find({ correo: { $regex: "@(?!gmail|outlook|hotmail)", $options: "i" } })
```

Ayuda a segmentar clientes con dominios personalizados, potencialmente empresariales.

### Consulta 19: Comentarios de crédito con menciones a "Riesgo"

```js
db.solicitudes_credito.find({ comentarios: { $regex: "Riesgo", $options: "i" } })
```

Revela comentarios sobre Riesgo en la solicitud de crédito.

### Consulta 20: Cuentas cuyo número empiece por "1"

```js
db.cuentas.find({ numero_cuenta: { $regex: "^1" } })
```

Ayuda a identificar cuentas creadas dentro de un mismo rango institucional.

### Consulta 21: Clientes que Terminen con una letra o espacio

```js
db.clientes.find({ nombre: { $regex: "^[A-Za-z ]+$" } })
```

Permite detectar errores de digitación o normalización de datos.

### Consulta 22: Solicitudes Aprobado con comentarios que mencionan "insuficientes"

```js
db.solicitudes_credito.find({ comentarios: { $regex: "insuficientes", $options: "i" }, estado: "Aprobado" })
```

Útil para estudiar causas comunes de rechazo.

### Consulta 23: Empleados con nombres que contienen la letra "o"

```js
db.empleados.find({ nombre: { $regex: "o", $options: "i" } })
```

Filtra empleados con nombres como "Yamile", "Yerson", "Mayra".

### Consulta 24: Clientes cuyo correo incluya un número

```js
db.clientes.find({ correo: { $regex: "\\d+" } })
```

Sirve para validar si el correo fue generado automáticamente o por usuario.

### Consulta 25: Transacciones que contengan palabras como "Transferencia" o "Compra"

```js
db.transacciones.find({ descripcion: { $regex: "Transferencia|Compra", $options: "i" } })
```

Permite identificar operaciones clave realizadas desde cajeros o apps móviles.

---

## Entregado

> Por: **jean marlon barajas**

> Fecha de entrega: 15 de junio de 2025
> Materia: Base de Datos NoSQL - Expresiones Regulares