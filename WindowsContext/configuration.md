# Configuración y despliegue local

## Dependencias principales
- Python 3.8+ (proyecto empacado con `pyproject.toml`, se instala con `pip install -e .`).
- Streamlit como interfaz web.
- MySQL (vía Docker Compose).
- `python-dotenv` para cargar variables de entorno.

## Variables de entorno (cargadas en `src/infrastructure/config.py`)
- `DB_HOST` (por defecto `localhost`)
- `DB_USER` (por defecto `user`)
- `DB_PASSWORD` (por defecto `password`)
- `DB_NAME` (por defecto `cosmitos_imperiales_db`)
- `EXCEL_REQUIRED_SHEETS` (lista separada por comas, por defecto `ATC,Encuesta salida`)
- `CSV_BASE_DIR` (por defecto `datos_analizados`)
- `APP_TITLE` (título mostrado en UI)

El archivo `.env` debe ubicarse en la raíz del repo y se carga automáticamente.

## Base de datos
- Levantamiento con `docker-compose up -d` (MySQL puerto 3306).
- Script inicial: `database_setup.sql` crea DB y tablas requeridas.

## Ejecución
- Iniciar app: `streamlit run src/app.py`.
- Detener DB: `docker-compose down` (usar `-v` para eliminar volúmenes/datos).
