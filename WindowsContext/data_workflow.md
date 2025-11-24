# Flujo de datos y ML

## Fuente de datos
- Archivos Excel en `excel_data/` con meses de encuestas (Enero-Junio 2025).
- CSV ya limpiados en `datos_analizados/` y `datos_excel/` (comentarios depurados).

## Preprocesamiento
- Limpiadores en `src/domain/services/` y adaptador `src/adapters/data_cleaner_adapter.py`.
- Patrones irrelevantes configurados en `comment_filter.py`; limpieza y normalización en `text_cleaner.py` y `word_cloud_service.py`.

## Clasificación de sentimiento
- Modelo sklearn serializado: `src/infrastructure/ML/clasificador_sentimiento_final.pkl` (copia original en `Model/`).
- El adaptador `src/adapters/sentiment_analyzer_adapter.py` convierte salidas a `Sentiment` mediante `use_cases/mappers/sentiment_mapper.py`.
- Fiabilidad/calidad de predicciones se calcula con `services/reliability_calculator.py`.

## Persistencia de análisis
- Repositorio en `src/adapters/repositories/analysis_repository_adapter.py` implementa `ports/analysis_repository.py` para guardar/listar/cargar/eliminar análisis.

## Visualización y exportación
- Tablas y gráficos: `src/infrastructure/ui/tables.py`, `charts.py`, `components/charts_component.py`.
- Nube de palabras: `components/word_cloud_component.py` apoyado en `word_cloud_service.py`.
- Exportación: `src/infrastructure/export.py` y `export_pdf.py`; UI en `components/export_component.py`.
