# Tablero de condición — Lavadora Electrolux W5250S

Proyecto final del Taller en Énfasis II (Gestión del Mantenimiento, Universidad de La Sabana, 2026-II).
Equipo: Juan Camilo Almario · Juan Diego Villalobos · Yesid Antonio.

Plataforma de seguimiento de condición del **motor de accionamiento del tambor** de la lavadora industrial Electrolux W5250S (caso Lavallena, Chorrillos, Lima). Usa el AMFEC, la curva P-F y las tareas de mantenimiento del grupo para decidir cuándo intervenir con base en datos.

## Cómo abrirlo

Abra `index.html` en un navegador con conexión a internet (carga Chart.js y SheetJS desde cdnjs). No requiere instalación.

Para publicarlo con GitHub Pages: Settings → Pages → rama `main`, carpeta raíz.

## Pestañas

| Pestaña | Contenido |
|---|---|
| Estado | Índice de salud 0–100, semáforo del equipo de 4 niveles y tarjetas de las 6 variables |
| Tendencias | Ajuste lineal o exponencial (mayor R²), tiempo hasta Alerta y Paro, comparación con el P-F neto |
| Alertas y acciones | Órdenes de trabajo sugeridas con modo de falla, tarea, prioridad, recurso y plazo |
| Indicadores de proceso | Disponibilidad, MTBF, MTTR y costo acumulado frente a sus metas |
| Datos y supuestos | Variables, umbrales con fuente, pesos, carga CSV/Excel, supuestos y limitaciones |

## Variables y umbrales

| Variable | Modo de falla | Normal | Precaución | Alerta (P) | Paro (antes de F) |
|---|---|---|---|---|---|
| Vibración (mm/s RMS) | M6, M7 | < 0,71 | 0,71–1,8 | 1,8–4,5 | ≥ 4,5 |
| T rodamiento (°C) | M6 | < 60 | 60–70 | 70–80 | ≥ 80 |
| ΔT motor sobre ambiente (K) | M9, M1 | < 40 | 40–55 | 55–70 | ≥ 70 |
| Aislamiento (MΩ) | M10, M1 | > 100 | 100–20 | 20–5 | ≤ 5 |
| Corriente (% In) | M5, M4, M6 | < 90 | 90–100 | 100–115 | ≥ 115 |
| Velocidad en extracción (rpm) | M3, M2, M5 | > 690 | 690–670 | 670–640 | ≤ 640 |

Las fuentes de cada límite, los pesos del índice (NPR del AMFEC) y los supuestos están en la pestaña **Datos y supuestos**.

## Datos

- **Simulador:** 5 escenarios (normal, M6 rodamientos, M9 ventilación, M10 humedad en bornes, M3 correa), con ruido y degradación de condición normal hasta paro. Todo dato simulado se etiqueta como *Supuesto · simulado*.
- **Datos propios:** archivo CSV o Excel en formato largo `dia,variable,valor,origen` (variables: `vib, trod, dtm, ais, corr, rpm`; origen: Medido, Inferido o Supuesto).
- **Indicadores:** CSV o Excel con `mes,horas_programadas,horas_paro,fallas,horas_reparacion,costo_mant,origen`.

## Demostración de normal a paro

Escenario *M6 · Desgaste de rodamientos* → **Reproducir**. La vibración pasa a Precaución cerca del día 210, a Alerta (punto P) cerca del 270 y a Paro cerca del 300, antes de la falla funcional en el día 330.
