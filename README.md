# BusinessSim

Modelo en Excel para simulacion de compras en EXSIM (Purchasing Manager).
Este repo esta pensado para usuarios finales: abrir el Excel, ajustar inputs y
obtener un plan de compra listo para cargar en la plataforma.

## Contenido del repositorio

- `EXSIM_Mezquite_Purchasing_CORREGIDO.xlsx`: modelo principal.
- `EXSIM Participants Guide.pdf`: guia del simulador (referencia).
- `production.xls`: datos de produccion (referencia).
- `raw_materials.xls`: datos de inventarios (referencia).
- `P_24_eC_02C.pdf`: material adicional del caso (referencia).

## Requisitos

- Microsoft Excel de escritorio recomendado (calculo completo y tablas).

## Uso rapido

1) Abre `EXSIM_Mezquite_Purchasing_CORREGIDO.xlsx`.
2) Ve a `Inputs` y ajusta:
   - Produccion planeada por quincena.
   - Inventario inicial (periodo base).
   - BOM (consumo por EC).
   - Batch size / precios / ordering / holding.
   - Proveedores elegidos para Parte A y Parte B.
3) Si quieres split por planta, edita `Multi_Planta`:
   - `Pct Centro (input)` permite forzar el reparto por material.
4) Recalcula (F9).
5) Revisa las salidas clave:
   - `BOM_Consumo`, `Inventario_Dinamico`, `MRP_NetReq`
   - `Compras_y_Lotes`, `Cashflow_Integrado`
   - `Analisis_Proveedores`, `Riesgo_Proveedor_B`
   - `BUYING_PLAN_FINAL`, `EXSIM_Upload`

## Salidas principales

- `BUYING_PLAN_FINAL`: plan de compra por planta y quincena (lotes, proveedor,
  costo esperado y pago).
- `EXSIM_Upload`: formato listo para copiar en la plataforma.

## Parametros ajustables

En `Inputs` hay un bloque **PLANNING PARAMETERS** para ajustar:

- Penalidad por stockout ($/EC).
- Costo financiero por quincena.
- Politica de revision y cobertura.
- Compra unica t=0 para piezas (1/0).

## Validaciones rapidas (sanity checks)

- Si EC=1000, Parte A debe consumir 1000 (no 200).
- Pieza 2 debe consumir 8x EC.
- Precios por batch de piezas: 60, 7, 36, 24, 30, 28.
- Si compras piezas en t=0, el cashflow inicial debe reflejar el golpe.

## Notas

- Supplier B tiene riesgo de no entrega (20%) y descuento por umbral de lotes.
- Los descuentos se aplican por pedido (quincena/material/proveedor).
