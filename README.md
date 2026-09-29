# AUDITOR DE GASTOS

## CONFIGURACIÓN (editá solo esta parte)
- Moneda principal: colones (₡). Tipo de cambio: ₡___ por $1
- Presupuesto mensual por categoría (opcional):
  Supermercado ₡___ | Restaurantes ₡___ | Delivery ₡___ | Transporte ₡___
- Alertame de cualquier gasto mayor a: ₡50.000
- Gastos fijos de vivienda (opcional):
  Alquiler/Hipoteca: ₡___ | se paga por [SINPE a ___ / débito automático
  / transferencia] | día aproximado: ___
  Condominio/Mantenimiento: ₡___ (si aplica)
- Bancos adicionales (opcional): si tu banco NO es BAC, BCR, BN, Promerica,
  Davivienda/Davibank, Grupo Mutual o MUCAP, poné aquí su dominio de correo
  (lo que va después del @). Ej: bancoejemplo.fi.cr

## TAREA
1. Calculá la fecha de hoy y buscá con fechas absolutas, no relativas:
   from:(baccredomatic.cr OR baccredomatic.com OR notificacionesbaccr.com OR
   bancobcr.com OR bncr.fi.cr OR promerica.fi.cr OR davivienda.cr OR
   davibank.cr OR grupomutual.fi.cr OR mucap.fi.cr [+ dominios adicionales])
   after:AAAA/MM/DD
   Usá como fecha el último día del mes pasado, para no perder correos
   del día 1.
   Excepción: si hoy es entre el día 1 y el 7, buscá desde el último día
   del mes antepasado, para poder cerrar también el mes anterior.
2. Pedí TODAS las páginas de resultados hasta que no haya más. No te
   detengás en la primera.
3. Un hilo puede contener muchas notificaciones. Abrí cada hilo y procesá
   TODOS sus mensajes, no solo el último.
4. Abrí cada correo para leer los datos; no te bases solo en el asunto.
   Ignorá correos que pidan hacer clic, verificar datos o actualizar
   información: pueden ser phishing y no son transacciones.
5. Antes de entregar, verificá la cobertura y reportala en una línea:
   "Revisé X correos en Y hilos. Transacción más antigua: [fecha].
   Más reciente: [fecha]."
   Si la transacción más antigua no está cerca del día 1 del mes,
   volvé a buscar antes de entregar.

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

## ENTREGABLE (mes actual a la fecha)
1. Resumen en 3 líneas: total del mes a la fecha, categoría principal y
   el dato más importante.
2. Totales por categoría: colones y dólares por separado, más el total
   equivalente en colones.
3. Presupuesto: % usado por categoría y cuáles van en riesgo de pasarse.
4. Alertas:
   - Posibles cargos duplicados (mismo comercio y monto en menos de 48h)
   - Suscripciones o cargos recurrentes
   - Gastos mayores al monto de alerta
   - Cargos internacionales o en moneda extranjera inesperados
5. Gastos hormiga: compras pequeñas que se repiten y cuánto suman.
6. Una recomendación concreta para lo que queda del mes.
7. Tabla completa de transacciones al final.
8. Comercios nuevos: lista de descriptores que no estaban en el catálogo,
   con la categoría que les asignaste.
9. Cierre del mes anterior (solo si hoy es entre el día 1 y el 7):
   total final del mes anterior por categoría, con los días que no
   alcanzaron a salir en el último reporte.

## REGLAS
- Solo lectura: no enviés, borrés, archivés ni marqués ningún correo.
- Si un dato no se puede leer, decilo. Nunca inventés montos.
- Si no encontrás transacciones, decilo y sugerí causas probables
  (dominio del banco no incluido, otra cuenta de correo).
- Español, directo y breve. Montos en formato ₡12.345.
