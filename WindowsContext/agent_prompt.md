# Prompt sugerido para Antigravity IDE

Usa este prompt en el agente integrado para que comprenda el proyecto "Cosmitos Imperiales / GSSP" y genere o actualice los archivos de contexto cuando se integren nuevas features.

---

**Contexto del proyecto:**
- App Streamlit que analiza comentarios de clientes usando un modelo de sentimiento entrenado (`src/infrastructure/ML/clasificador_sentimiento_final.pkl`).
- Arquitectura Limpia con capas `infrastructure → adapters → use_cases → domain` (dependencias hacia adentro).
- Base de datos MySQL levantada con `docker-compose.yml` (DB: `cosmitos_imperiales_db`, usuario `user`, password `password`), script inicial `database_setup.sql`.
- Datos de entrada: encuestas en `excel_data/` y CSV limpios en `datos_analizados/`.
- Entrypoint: `src/app.py` (Streamlit) que usa el contenedor de dependencias `src/infrastructure/dependency_injection_container.py`.
- Casos de uso clave: procesamiento de archivo, preparación de visualizaciones, generación de resúmenes, CRUD de análisis.
- UI modular en `src/infrastructure/ui/components/` (upload, tablas, charts, export, sidebar, word cloud) coordinada por `ui/controllers/streamlit_controller.py`.
- Configuración vía `.env` leída en `src/infrastructure/config.py` (host/credenciales DB, hojas Excel requeridas, carpeta CSV, título UI).

**Instrucciones para el agente:**
1. **Respetar la arquitectura**: nuevas dependencias deben entrar por adaptadores; los casos de uso solo conocen puertos; el dominio permanece puro.
2. **Mantener coherencia de datos**: validar hojas requeridas (`EXCEL_REQUIRED_SHEETS`), usar `CSV_BASE_DIR` para salidas y reutilizar `Sentiment` del dominio.
3. **Extender la UI** mediante componentes en `infrastructure/ui/components/` y orquestación en `streamlit_controller.py`.
4. **Persistencia**: seguir el contrato de `use_cases/ports/analysis_repository.py` al agregar nuevas estrategias de guardado/carga.
5. **Agregar documentación** en esta carpeta `WindowsContext` cuando se creen nuevas features (nuevos casos de uso, adaptadores, visualizaciones, configuraciones o scripts de datos).
6. **Pasos recomendados de ejecución local**: instalar deps con `pip install -e .`; levantar MySQL con `docker-compose up -d`; correr la app con `streamlit run src/app.py`.

**Salida esperada**
- Mantener/actualizar archivos de contexto en `WindowsContext/` (por ejemplo, `overview`, `architecture`, `modules`, `configuration`, nuevos resúmenes de features) para que otros agentes/colaboradores entiendan el estado actualizado.
