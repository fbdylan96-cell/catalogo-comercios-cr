# 💸 Auditor de Gastos Semanal con Claude

Un prompt que revisa tu Gmail cada semana, encuentra las notificaciones de compra de tu banco y te dice **en qué se te fue el dinero**: totales por categoría, alertas, gastos hormiga y una recomendación concreta.

Sin Excel. Sin anotar nada a mano.

---

## ✅ Qué necesitás

- **Claude** con plan de pago (Pro o superior)
- **Gmail** donde te lleguen las notificaciones de compra de tu banco

---

## ⚙️ Setup en 3 pasos

### 1. Conectá Gmail a Claude
En Claude, andá a **Configuración → Conectores → Gmail → Conectar** y autorizá la cuenta donde te llegan los correos del banco.

### 2. Probalo una vez a mano
Copiá el prompt de abajo, llená la sección **CONFIGURACIÓN** y pegalo en un chat nuevo de Claude. Revisá que el resultado tenga sentido antes de automatizarlo.

### 3. Programalo para cada lunes
- Si en Claude ves la opción **Cowork**: andá a **Scheduled → New task**, pegá el prompt y elegí **semanal, lunes 7:00 a.m.**
- Si no la ves: escribile a Claude en cualquier chat *"Programá esta tarea para todos los lunes a las 7 a.m."* y pegá el prompt.

Listo. Cada lunes vas a tener tu reporte esperándote.

---

## 📋 El prompt

Hacé click en el botón de copiar (arriba a la derecha del bloque).

```
# AUDITOR DE GASTOS SEMANAL

## CONFIGURACIÓN (editá solo esta parte)
- Bancos y remitentes: [ej: BAC - correo@..., BCR - correo@...]
  (si no sabés el remitente, poné solo el nombre del banco)
- Moneda principal: colones (₡). Tipo de cambio: ₡___ por $1
- Presupuesto mensual por categoría (opcional):
  Supermercado ₡___ | Restaurantes ₡___ | Delivery ₡___ | Transporte ₡___
- Alertame de cualquier gasto mayor a: ₡50.000
- Gastos fijos de vivienda (opcional):
  Alquiler/Hipoteca: ₡___ | se paga por [SINPE a ___ / débito automático
  / transferencia] | día aproximado: ___
  Condominio/Mantenimiento: ₡___ (si aplica)

## TAREA
Revisá mi Gmail y encontrá las notificaciones de transacciones desde el
día 1 del mes pasado hasta hoy. Abrí cada correo para leer los datos;
no te bases solo en el asunto.

INCLUIR: compras con tarjeta, cargos recurrentes, SINPE Móvil enviados,
pagos de servicios.
EXCLUIR: promociones, estados de cuenta, códigos de verificación, pagos
a mi propia tarjeta de crédito y transferencias entre mis propias cuentas.
Las reversiones listalas aparte.

De cada transacción extraé: fecha, comercio, monto, moneda, banco y
últimos 4 dígitos de la tarjeta.

## CATEGORIZACIÓN
Categorías: Supermercado, Restaurantes, Delivery, Transporte/Combustible,
Suscripciones, Servicios, Salud, Compras, Entretenimiento, Vivienda,
SINPE/Transferencias, Otros.

Aplicá estos pasos en orden:
1. Catálogo: descargá
   https://raw.githubusercontent.com/fbdylan96-cell/catalogo-comercios-cr/refs/heads/main/catalogo.csv
   Si el descriptor del comercio contiene un patrón del catálogo, usá esa
   categoría y ese nombre de comercio. Si varios patrones coinciden, usá
   el más largo.
2. Palabras clave (si no está en el catálogo):
   - RESTAURANTE, SODA, PIZZERIA, CAFETERIA → Restaurantes
   - SUPERMERCADO, MINI SUPER, MINISUPER, PULPERIA → Supermercado
   - SERVICENTRO, GASOLINERA, PARQUEO, PARKING, PEAJE → Transporte/Combustible
   - FARMACIA, CLINICA, LABORATORIO, HOSPITAL → Salud
   - FERRETERIA, LIBRERIA → Compras
   - ALQUILER, HIPOTECA, CONDOMINIO, MANTENIMIENTO → Vivienda
     (revisá también la descripción o motivo del SINPE o la transferencia,
     no solo el destinatario)
3. Tu criterio: si nada aplica, categorizá con tu mejor criterio, marcalo
   con (?) y agregalo a la sección "Comercios nuevos".
Si no podés descargar el catálogo, avisalo y seguí con los pasos 2 y 3.

Vivienda: si una transferencia, SINPE o débito coincide con los gastos
fijos de vivienda configurados (monto similar y fecha cercana),
categorizala como Vivienda aunque sea transferencia. Si el pago
configurado no aparece en los correos, incluilo en los totales del mes
como "declarado (no detectado)".

## ENTREGABLE (enfocado en los últimos 7 días)
1. Resumen en 3 líneas: total de la semana, categoría principal y el
   dato más importante.
2. Totales por categoría: colones y dólares por separado, más el total
   equivalente en colones.
3. Presupuesto: % usado del mes a la fecha por categoría y cuáles van
   en riesgo de pasarse.
4. Comparación contra la semana anterior: qué subió y qué bajó.
   Excluí Vivienda de esta comparación (es un pago mensual), pero
   incluila en los totales y el presupuesto del mes.
5. Alertas:
   - Posibles cargos duplicados (mismo comercio y monto en menos de 48h)
   - Suscripciones o cargos recurrentes nuevos
   - Gastos mayores al monto de alerta
   - Cargos internacionales o en moneda extranjera inesperados
6. Gastos hormiga: compras pequeñas que se repiten y cuánto suman.
7. Una recomendación concreta para la próxima semana.
8. Tabla completa de transacciones al final.
9. Comercios nuevos: lista de descriptores que no estaban en el catálogo,
   con la categoría que les asignaste.

## REGLAS
- Solo lectura: no enviés, borrés, archivés ni marqués ningún correo.
- Si un dato no se puede leer, decilo. Nunca inventés montos.
- Si no encontrás transacciones, decilo y sugerí causas probables
  (remitente equivocado, otra cuenta de correo).
- Español, directo y breve. Montos en formato ₡12.345.
```

---

## ✏️ Ejemplo de configuración llena

```
## CONFIGURACIÓN
- Bancos y remitentes: BAC, BCR
- Moneda principal: colones (₡). Tipo de cambio: ₡510 por $1
- Presupuesto mensual por categoría:
  Supermercado ₡180.000 | Restaurantes ₡60.000 | Delivery ₡30.000 | Transporte ₡70.000
- Alertame de cualquier gasto mayor a: ₡50.000
- Gastos fijos de vivienda:
  Alquiler: ₡350.000 | se paga por SINPE | día aproximado: 1
```

No hace falta llenar todo. Si dejás algo en blanco, Claude lo omite.

---

## 🗂️ El catálogo de comercios

[`catalogo.csv`](catalogo.csv) tiene comercios comunes en Costa Rica con su categoría, para que Claude no tenga que adivinar con descriptores como "AMPM", "PALI" o "UBER EATS".

**¿Te aparecieron comercios nuevos?** Al final de cada reporte Claude te los lista. Mandámelos por DM a **@dylanmosqc** y los agrego al catálogo para todos.

---

## 🔒 Aviso

- El prompt es **solo lectura**: Claude no envía, borra ni modifica tus correos.
- Tus datos quedan entre tu Gmail y tu cuenta de Claude. Este repo no recibe ni guarda nada tuyo.
- Revisá siempre los números contra tus estados de cuenta. Es una herramienta de organización, no asesoría financiera.

---

Hecho por **@dylanmosqc** · Si te sirvió, compartilo con alguien que todavía anota sus gastos en Excel.
