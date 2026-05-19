# API CotizAR - Backend de Instrumentos Financieros

Este repositorio contiene el desarrollo de una API REST funcional e integral construida sobre **FastAPI**, diseñada para la extracción, persistencia, procesamiento y exposición de cotizaciones de activos e instrumentos del mercado financiero argentino en tiempo real. 

El sistema soporta ejecución modular en entornos locales y despliegue distribuido mediante contenedores de software. El proyecto fue desarrollado en el marco de la carrera de Ciencia de Datos (UNSAM).

---

## 1. Características Técnicas de la API

* **Módulo de Web Scraping Automático:** Componentes independientes (`source/`) encargados de la ingesta automatizada de datos financieros crudos desde fuentes públicas (bandas cambiarias, letras de vencimiento, plazos fijos bancarios, cotización del dólar y bonos soberanos de renta fija).
* **Subsistema de Autenticación y Seguridad:** Capa de seguridad (`auth/`) que implementa control de acceso, persistencia de usuarios y generación controlada de perfiles administradores iniciales.
* **Diseño Orientado a Dominio (Models):** Representación abstracta e intermedia de los instrumentos del mercado argentino (`instruments.py`, `alerta.py`) y uso de interfaces de abstracción para motores de bases de datos (`abstract_db.py`).
* **Arquitectura de Notificaciones (Alertas):** Implementación de lógica orientada a eventos para gatillar alertas personalizadas ante variaciones críticas en la cotización de activos y rupturas de bandas cambiarias.
* **Infraestructura de Despliegue:** Contenedorización completa mediante un archivo `Dockerfile` optimizado y configuración de exclusiones con `.dockerignore` para despliegues continuos (CD) automatizados en la nube (Render).

---

## Estructura del Proyecto

```text
└── Proyecto/               # Arquitectura principal de la API CotizAR
    ├── auth/               # Módulos de autenticación y tokenización de accesos
    ├── datasets/           # Almacenamiento local de series financieras temporales (CSV)
    ├── db/                 # Controladores y abstracciones de bases de datos
    ├── factory/            # Fábricas de instrumentos de renta fija
    ├── models/             # Modelos de datos del dominio financiero y objetos sujeto
    ├── routers/            # Endpoints y controladores de enrutamiento web
    ├── source/             # Pipelines de web scraping y extracción de datos
    ├── tests/              # Pruebas de integración sobre autenticación e instrumentos
    └── Dockerfile          # Configuración del contenedor Docker para producción
