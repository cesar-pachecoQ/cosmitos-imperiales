# Arquitectura y capas

El proyecto sigue **Arquitectura Limpia** con dependencias apuntando hacia el dominio. Orden de capas (de externo a interno):

```
Infrastructure → Adapters → Use Cases → Domain
```

## Capa Dominio (`src/domain`)
- **Entidades**: `Review`, `AnalyzedReview` en `entities/review.py`.
- **Objetos de valor**: `Sentiment` (enum: Detractor, Neutro, Promotor) en `value_objects/sentiment.py`.
- **Servicios de negocio**: limpieza de texto, filtrado de comentarios irrelevantes, cálculo de métricas y fiabilidad, preparación de corpus para nubes de palabras.

## Casos de Uso (`src/use_cases`)
- Orquestan flujos de aplicación sin depender de frameworks.
- Principales: `process_file_use_case`, `prepare_analysis_display_use_case`, `generate_summary_use_case`, `list_analyses_use_case`, `load_analysis_use_case`, `delete_analysis_use_case`, `read_file_use_case`.
- Definen puertos/abstracciones en `ports/` para repositorios, cleaners, file readers y analizadores de sentimiento.

## Adaptadores (`src/adapters`)
- Implementan puertos de casos de uso.
- **Lectura**: `file_readers/file_reader_adapter.py`.
- **Limpieza**: `data_cleaner_adapter.py` (normaliza/filtra datos).
- **Persistencia**: `repositories/analysis_repository_adapter.py` (gestiona análisis guardados).
- **ML**: `sentiment_analyzer_adapter.py` (usa modelo `clasificador_sentimiento_final.pkl`).

## Infraestructura (`src/infrastructure`)
- **Config**: `config.py` carga `.env` (host/credenciales DB, hojas requeridas, carpeta CSV, título UI).
- **Dependencia/DI**: `dependency_injection_container.py` cablea adaptadores, servicios y casos de uso.
- **UI Streamlit**: componentes en `infrastructure/ui/components/` (carga de archivos, tablas, gráficas, exportación, sidebar, nube de palabras) coordinados por `controllers/streamlit_controller.py`.
- **Exportación**: `export.py`, `export_pdf.py`, `tables.py`, `charts.py`, `sidebar.py`, constantes en `constants.py`.

## Flujo alto nivel
1. Usuario carga archivo (Excel/CSV) vía Streamlit.
2. Caso de uso lee y limpia datos a través de adaptadores.
3. Analizador de sentimientos calcula clasificación y fiabilidad.
4. Métricas y visualizaciones se generan en servicios y se muestran en UI; resultados pueden exportarse/guardarse.
5. Análisis se listan, cargan y eliminan mediante repositorio y casos de uso dedicados.

## Puntos de extensión
- Añadir nuevas fuentes de datos creando adaptadores que implementen `ports/file_reader.py`.
- Reemplazar el modelo de ML actual proporcionando otro adaptador de `ports/sentiment_analyzer.py`.
- Introducir nuevas visualizaciones en `infrastructure/ui/components/` consumiendo los casos de uso existentes.
