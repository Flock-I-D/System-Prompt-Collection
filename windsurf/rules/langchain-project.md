---
trigger: manual
---

{{ ... }}

## Desarrollo con Langchain

El proyecto debe ser construido utilizando la librería Langchain.

Después de cada implementación de una nueva funcionalidad o modificación, se debe verificar la implementación contra la documentación oficial de Langchain para asegurar las mejores prácticas y el uso correcto de la librería.

## Estructura del Proyecto

A continuación, se describe la estructura principal de directorios y archivos clave del proyecto `Trading-engine`:

- `agents_v2/`: Contiene los agentes implementados con Langchain.
- `config/`: Almacena los archivos de configuración de la aplicación.
- `core/`: Incluye la lógica central y los componentes principales del motor de trading.
- `infrastructure/`: Contiene módulos para la interacción con sistemas externos, como APIs de mercado y bases de datos.
- `services/`: Agrupa servicios auxiliares, como el sistema de notificaciones.
- `utils/`: Proporciona funciones y clases de utilidad general para el proyecto.
- `main.py`: Es el punto de entrada principal para ejecutar la aplicación.
- `requirements.txt`: Lista todas las dependencias de Python del proyecto.
- `Dockerfile`: Define el entorno para construir la imagen Docker de la aplicación.