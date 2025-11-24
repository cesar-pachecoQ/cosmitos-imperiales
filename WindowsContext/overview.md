# Cosmitos Imperiales / GSSP - Resumen rápido

Este proyecto implementa el **Gestor de Satisfacción y Seguimiento de Posventa (GSSP)**, una aplicación Streamlit para analizar comentarios de clientes mediante un clasificador de sentimientos de ML. Sigue **Arquitectura Limpia** con separaciones claras entre Dominio, Casos de Uso, Adaptadores e Infraestructura. Usa MySQL vía Docker Compose y lee/limpia datos de encuestas en Excel/CSV.

## Objetivos principales
- Cargar archivos de encuestas de satisfacción y preprocesarlos (limpieza, filtrado, normalización).
- Clasificar sentimientos y calcular métricas/fiabilidad.
- Visualizar resultados (tablas, gráficas, nubes de palabras) y exportarlos (PDF/Excel).
- Persistir y gestionar análisis realizados (listar, cargar, eliminar).

## Entradas de datos
- Hojas Excel ubicadas en `excel_data/` y CSV preprocesados en `datos_analizados/`.
- Configuración opcional mediante `.env` (host, usuario, contraseña y DB de MySQL, hojas requeridas, carpeta base de CSV).

## Ejecución resumida
1) Activar entorno y `pip install -e .`.
2) Levantar MySQL con `docker-compose up -d` (se autoejecuta `database_setup.sql`).
3) Iniciar la app: `streamlit run src/app.py`.

## Activos clave
- Documento de arquitectura: `architecture_overview.md`.
- Configuración DB: `database_setup.sql` y `docker-compose.yml`.
- Modelo ML empaquetado: `src/infrastructure/ML/clasificador_sentimiento_final.pkl`.
- Notebooks de exploración/modelado: carpeta `model/` y `Model/`.
