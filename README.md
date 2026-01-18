# 🚀 Proceso ETL de Datos con SQL Server Integration Services (SSIS)

## Descripción del Proyecto

Este proyecto se centra en la implementación de un robusto proceso ETL (Extracción, Transformación y Carga) utilizando **Microsoft SQL Server Integration Services (SSIS)**. Su objetivo primordial es orquestar la migración y consolidación de datos desde una base de datos transaccional de origen, como `BDVentas`, hacia un **Data Warehouse (DW)** de destino. Se emplea una arquitectura de dos esquemas: `staging` para la preparación, limpieza y validación intermedia de los datos, y `dw` para el almacenamiento final, optimizado para análisis y reportes.

Este enfoque asegura la calidad e integridad de los datos antes de su consolidación, facilitando la toma de decisiones basada en información fiable.

## ✨ Características Principales

*   ✅ **Automatización de ETL**: Proporciona una solución robusta y escalable para automatizar la transferencia y transformación de datos, reduciendo errores manuales y optimizando tiempos.
*   🔄 **Extracción, Transformación y Carga**: Implementa las fases clave de ETL para conectar, procesar y cargar datos de manera eficiente desde una base de datos SQL de origen.
*   🛡️ **Uso de Staging Area**: Incorpora un esquema `staging` intermedio, fundamental para aplicar validaciones, limpiezas y transformaciones complejas, garantizando la calidad de los datos antes de su carga final al Data Warehouse.
*   📊 **Integración de Datos para BI**: Facilita la consolidación de información de diversas fuentes en un repositorio centralizado, esencial para herramientas de Business Intelligence y análisis.
*   🧩 **Diseño Modular con SSIS**: Utiliza paquetes SSIS (`.dtsx`) para estructurar el flujo de datos de manera modular y mantenible, permitiendo una fácil expansión y depuración.

## ⚙️ Requisitos Previos

Para desarrollar, ejecutar y desplegar este proyecto, necesitarás los siguientes componentes:

*   **Microsoft SQL Server**:
    *   Una instancia de SQL Server que albergue la base de datos de origen (e.g., `BDVentas`).
    *   Una instancia de SQL Server que contenga el Data Warehouse de destino (e.g., `DW`), con los esquemas `staging` y `dw` ya creados y configurados.
*   **SQL Server Data Tools (SSDT)** o **Visual Studio**:
    *   Se requiere **Visual Studio** con la extensión "SQL Server Integration Services Projects" instalada. Esta es la herramienta principal para el desarrollo y depuración de soluciones SSIS.
*   **Conocimientos Básicos**:
    *   Familiaridad con el lenguaje SQL (DDL y DML).
    *   Comprensión de los conceptos fundamentales de procesos ETL y modelado de Data Warehouses.

## 🚀 Instrucciones de Instalación

Sigue estos pasos para poner en marcha el proyecto en tu entorno:

1.  ⬇️ **Clonar el Repositorio**:
    ```bash
    git clone https://github.com/alejav0240/proceso-ETL.git
    cd proceso-ETL
    ```

2.  ⚙️ **Configurar Bases de Datos**:
    Asegúrate de que tus instancias de SQL Server contengan:
    *   La base de datos de origen, por ejemplo, `BDVentas`, con los datos que deseas extraer.
    *   La base de datos del Data Warehouse, por ejemplo, `DW`, con los esquemas `staging` y `dw` listos para recibir los datos.
    *   Verifica que las credenciales de acceso para ambas bases de datos sean correctas y tengan los permisos necesarios.

3.  📂 **Abrir el Proyecto SSIS**:
    *   Abre el archivo de solución `ETL.sln` con Visual Studio.
    *   Dentro del proyecto SSIS, localiza los "Administradores de Conexión" (`.conmgr` files, como `DESKTOP-4V64PMS.BDVentas.conmgr` y `DESKTOP-4V64PMS.DW.conmgr`).
    *   **Es crucial** que edites estos administradores de conexión para que apunten a tus bases de datos de origen y destino específicas. Esto implica actualizar el nombre del servidor, la base de datos y las credenciales si es necesario.

4.  📦 **Desplegar el Proyecto (Opcional)**:
    Una vez configurado y probado, puedes desplegar el proyecto SSIS en el Catálogo de SSIS de tu instancia de SQL Server. Esto permite su ejecución programada a través de SQL Server Agent Jobs o su ejecución manual mediante SQL Server Management Studio (SSMS).

## 👨‍💻 Guía de Uso

El corazón de este proceso ETL reside en el paquete principal, `Package.dtsx`.

1.  ▶️ **Ejecutar desde Visual Studio**:
    *   Abre el archivo `Package.dtsx` en Visual Studio.
    *   Puedes ejecutar el paquete directamente desde el entorno de desarrollo (presionando F5 o el botón "Iniciar") para probar el flujo de datos, depurar y verificar su correcto funcionamiento.

2.  📅 **Ejecutar desde SQL Server (Catálogo SSIS)**:
    *   Si has desplegado el proyecto en el Catálogo de SSIS (en SSMS, bajo "Integration Services Catalogs"), puedes ejecutar el paquete de forma ad-hoc.
    *   Para automatización, crea un SQL Server Agent Job que invoque la ejecución del paquete SSIS en intervalos definidos.

### Ejemplo de Flujo General del Proceso ETL

El paquete `Package.dtsx` está diseñado para orquestar la siguiente secuencia de tareas:

*   **1. 📥 Tarea de Extracción**: Se conecta a la base de datos de origen (`BDVentas`) y extrae los datos relevantes de las tablas transaccionales.
*   **2.  staging ➡️ Tarea de Staging**: Los datos extraídos se cargan en tablas temporales dentro del esquema `staging` del Data Warehouse (`DW`). Aquí se realiza una primera fase de limpieza y preparación.
*   **3. ⚙️ Tarea de Transformación**: Se aplican reglas de negocio, validaciones, limpieza de datos, agregaciones y otras lógicas de transformación a los datos que residen en el esquema `staging`.
*   **4. ⬆️ Tarea de Carga Final**: Los datos ya transformados y validados se mueven desde el esquema `staging` al esquema `dw` del Data Warehouse, donde quedan disponibles para análisis.

## 🌳 Estructura del Proyecto
```
proceso-ETL/
├── ETL/
│   ├── bin/
│   │   └── Development/
│   │       └── ETL.ispac          # Paquete de despliegue de SSIS
│   ├── obj/
│   │   └── Development/
│   │       ├── BuildLog.xml
│   │       ├── DESKTOP-4V64PMS.BDVentas.conmgr  # Administrador de Conexión a BDVentas
│   │       ├── DESKTOP-4V64PMS.DW.conmgr       # Administrador de Conexión a Data Warehouse
│   │       ├── ETL.dtproj                     # Archivo de proyecto SSIS
│   │       ├── Package.dtsx                   # Paquete principal de ETL
│   │       └── Project.params                 # Parámetros del proyecto
│   ├── DESKTOP-4V64PMS.BDVentas.conmgr       # Administrador de Conexión a BDVentas (duplicado para proyecto)
│   ├── DESKTOP-4V64PMS.DW.conmgr            # Administrador de Conexión a Data Warehouse (duplicado para proyecto)
│   ├── ETL.database
│   ├── ETL.dtproj                           # Archivo de proyecto SSIS
│   ├── ETL.dtproj.user
│   ├── Package.dtsx                         # Paquete principal de ETL
│   └── Project.params                       # Parámetros del proyecto
└── ETL.sln                                # Archivo de solución de Visual Studio
```

## 💻 Tecnologías Utilizadas

*   **Microsoft SQL Server Integration Services (SSIS)**: La herramienta principal para el diseño y ejecución de los flujos ETL.
*   **Microsoft SQL Server**: La plataforma de base de datos utilizada tanto para el origen de datos (`BDVentas`) como para el Data Warehouse de destino (`DW`).