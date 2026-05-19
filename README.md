# API CotizAR y Catálogo de Patrones de Diseño en Python

Este repositorio contiene el desarrollo de un backend integral para el procesamiento, consulta y alerta de instrumentos financieros del mercado argentino, complementado con una colección de implementaciones prácticas de patrones de diseño orientados a objetos. Todo el contenido fue desarrollado en el marco de la cursada de Programación 2 para la Licenciatura en Ciencia de Datos (UNSAM).

---

## 1. Proyecto Core: API CotizAR (Motor Financiero)

La carpeta `Proyecto/` contiene una API REST funcional construida sobre **FastAPI**, diseñada para la extracción, persistencia y exposición de cotizaciones de activos e instrumentos financieros en tiempo real. El sistema soporta ejecución local modular y despliegue distribuido mediante contenedores.

### Características Técnicas de la API
* **Módulo de Web Scraping Automático:** Scripts desacoplados (`source/`) encargados de la ingesta de datos financieros crudos desde fuentes públicas (bandas cambiarias, letras de vencimiento, plazos fijos bancarios, cotización del dólar y bonos soberanos).
* **Subsistema de Autenticación y Seguridad:** Capa de seguridad (`auth/`) que implementa control de acceso, persistencia de usuarios y generación de perfiles administradores iniciales de forma segura.
* **Diseño Orientado a Dominio (Models):** Representación abstracta e intermedia de los instrumentos del mercado argentino (`instruments.py`, `alerta.py`) y uso de interfaces de abstracción para motores de bases de datos (`abstract_db.py`).
* **Arquitectura de Notificaciones (Alertas):** Implementación del patrón Observer (`dolar_subject.py`) dentro de la lógica del negocio para gatillar alertas personalizadas ante variaciones en la cotización de activos y bandas cambiarias.
* **Infraestructura de Despliegue:** Contenedorización completa mediante un archivo `Dockerfile` optimizado y configuración de archivos `.dockerignore` para despliegues continuos automatizados en plataformas Cloud como Render.

---

## 2. Catálogo de Patrones de Diseño de Software

Fuera del módulo principal, el repositorio incluye una suite de diseño de software basada en los patrones presentados en *Head First Design Patterns*, enfocados en los principios SOLID (con énfasis en el Open-Closed Principle).

### Patrón Factory (Creación de Objetos)
Ubicado en `factory/`, el módulo aborda la evolución de la instanciación de objetos en tres niveles arquitectónicos utilizando cuadernos analíticos de Jupyter para su documentación:
* **Simple Factory:** Desacoplamiento básico de la creación de tipos en una clase fábrica centralizada.
* **Factory Method:** Delegación de la responsabilidad de instanciación a las subclases a través de métodos abstractos.
* **Abstract Factory:** Creación de familias de objetos dependientes (ingredientes y componentes) sin especificar sus clases concretas.

### Patrón Decorator (Extensión Dinámica)
Ubicado en `decorator/`, implementa la composición dinámica de comportamientos (envoltura) en tiempo de ejecución. Incluye extensiones avanzadas desarrolladas fuera de la consigna base, tales como:
* **Builder de Bebidas (`build_beverage.py`):** Una interfaz fluida para abstraer la complejidad de la concatenación manual de decoradores.
* **Pretty Print (`PrettyPrint.py`):** Un formateador abstracto a nivel de texto encargado de procesar y compactar la cadena de descripciones sin alterar la lógica matemática de costos del negocio.

### Patrón Observer (Sistemas Event-Driven)
Ubicado en `observer/`, modela una arquitectura desacoplada uno-a-muchos (Weather Station). Contiene la documentación técnica y código base para la refactorización estructural del modelo de distribución de estado "Push" hacia el modelo optimizado de consulta selectiva "Pull".

---

## Estructura General del Repositorio

```text
├── Proyecto/               # Arquitectura de la API CotizAR (FastAPI + Docker)
│   ├── auth/               # Módulos de autenticación y tokenización de accesos
│   ├── datasets/           # Almacenamiento local de series financieras temporales (CSV)
│   ├── db/                 # Controladores y abstracciones de bases de datos
│   ├── factory/            # Fábricas de instrumentos de renta fija
│   ├── models/             # Modelos de datos del dominio financiero y objetos sujeto
│   ├── routers/            # Endpoints y controladores de enrutamiento web
│   ├── source/             # Pipelines de web scraping y extracción de datos
│   ├── tests/              # Pruebas de integración sobre autenticación e instrumentos
│   └── Dockerfile          # Configuración del contenedor Docker para producción
├── factory/                # Implementaciones analíticas de patrones de fábrica
├── decorator/              # Implementación avanzada del patrón Decorator con wrappers
└── observer/               # Implementación del patrón Observer (Modelos Push y Pull)
