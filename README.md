# Caso 1 · Pronóstico de ventas Walmart
Primer caso de estudio de **Estadística Aplicada (14134), segundo semestre 2026 — USACH**.

Análisis en R de ventas agregadas por tienda y semana. El objetivo es pronosticar una semana hacia adelante utilizando observaciones disponibles hasta la semana anterior.

## Organización
| Ruta | Contenido |
| --- | --- |
| `codigo/walmart_analysis.R` | Script principal |
| `datos/train.csv` | Ventas históricas por departamento |
| `datos/features.csv` | Variables de contexto |
| `datos/stores.csv` | Información de tiendas |
| `docs/instrucciones_de_uso.txt` | Guía de ejecución y salidas |
| `resultados/` | Salidas generadas al ejecutar; excluidas de Git |

## Ejecutar
Se requiere R y los paquetes `rpart`, `randomForest`, `gbm` y `glmnet`.
Instalarlos una vez desde R:

```r
install.packages(c("rpart", "randomForest", "gbm", "glmnet"))
```

Desde una terminal ubicada en la raíz del repositorio:

```sh
Rscript codigo/walmart_analysis.R
```

También puedes abrir el script en RStudio. La detección de la ruta del documento requiere el paquete opcional `rstudioapi` y que el documento esté guardado; la ejecución con Rscript es la opción más directa.

Las variables de entorno `WALMART_DATA_DIR` y `WALMART_RESULTS_DIR` permiten cambiar las rutas de datos y resultados.

## Flujo del análisis
- Agregación de ventas a tienda-semana y auditoría de claves y calendario.
- Predictores rezagados y medias móviles calculadas con historia hasta t−1.
- Validación temporal para hiperparámetros, selección cronológica, calibración y test final.
- Comparación de modelos lineales, regularizados, spline, árbol, random forest, boosting, promedio y baselines.
- Exportación de métricas, diagnósticos, interpretabilidad, intervalos empíricos y modelos.

El protocolo evalúa predicciones semanales con rezagos observados, sin reentrenamiento durante test. Los intervalos son empíricos: su cobertura debe revisarse en las salidas, sin asumir una garantía bajo dependencia temporal.

## Resultados
El script crea `resultados/`, con tablas CSV, textos, gráficos en `graficos/` y objetos RDS en `binarios/`. Consulta `resumen.csv`, `test_modelo_y_baseline.csv` y `controles_pipeline.csv` después de ejecutar.

No se incluyen métricas ni se afirma una ejecución verificada en esta reorganización. Los archivos de datos y la lógica estadística del script se conservaron.

## Datos
Se conservan los CSV incorporados al proyecto Walmart. La URL de origen y las condiciones de uso deben documentarse antes de redistribuirlos fuera del contexto del curso.
