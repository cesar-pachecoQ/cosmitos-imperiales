# Módulos y responsabilidades

## Dominio (`src/domain`)
- `entities/review.py`: entidades `Review` y `AnalyzedReview`.
- `value_objects/sentiment.py`: enum `Sentiment` con helpers de conversión.
- `services/`: utilidades de negocio (limpieza de texto, filtrado, métricas, fiabilidad, preparación de nubes de palabras).

## Casos de uso (`src/use_cases`)
- `process_file_use_case.py`: orquesta lectura, limpieza y análisis de archivo cargado.
- `prepare_analysis_display_use_case.py`: prepara datos ya analizados para visualización.
- `generate_summary_use_case.py`: crea resumen de resultados y métricas.
- `list_analyses_use_case.py`, `load_analysis_use_case.py`, `delete_analysis_use_case.py`: CRUD de análisis persistidos.
- `read_file_use_case.py`: lectura pura de archivos soportados.
- `mappers/sentiment_mapper.py`: conversión de resultados del modelo a objetos de dominio.
- `ports/`: interfaces para repositorio, limpiador, lector de archivos y analizador de sentimiento.

## Adaptadores (`src/adapters`)
- `file_readers/file_reader_adapter.py`: lee fuentes (Excel/CSV) y las normaliza al formato esperado.
- `data_cleaner_adapter.py`: aplica limpieza y filtrado definidos en dominio.
- `repositories/analysis_repository_adapter.py`: persistencia de análisis (archivo/DB según implementación interna).
- `sentiment_analyzer_adapter.py`: carga y ejecuta modelo de sentimiento `clasificador_sentimiento_final.pkl`.

## Infraestructura (`src/infrastructure`)
- `config.py`: carga variables de entorno y expone `Settings`.
- `dependency_injection_container.py`: instancia y conecta adaptadores, servicios y casos de uso.
- `ML/`: modelo serializado de sentimiento.
- `ui/controllers/streamlit_controller.py`: entrypoint UI, coordina componentes y casos de uso.
- `ui/components/`: piezas de UI (upload, tablas, gráficas, sidebar, exportación, nubes de palabras, manejo de estado).
- `export.py`, `export_pdf.py`, `tables.py`, `charts.py`, `sidebar.py`: helpers para visualización/exportación.
- `constants.py`: textos/etiquetas reutilizables.

## Aplicación (`src/app.py`)
- Punto de entrada Streamlit; inicializa contenedor DI y arranca controlador UI.

## Datos y modelos
- Datos crudos en `excel_data/`, derivados limpios en `datos_analizados/` y `datos_excel/`.
- Notebooks de exploración/modelado en `model/` y `Model/`.
- Modelo entrenado `Model/clasificador_sentimiento_final.pkl` y copia de uso en `src/infrastructure/ML/`.
