## Descripción funcional del sistema

El sistema **EIEInfo** es la plataforma web oficial de la Escuela de Ingeniería Eléctrica (EIE) de la Universidad de Costa Rica. Su propósito es centralizar y facilitar el acceso a información institucional, administrativa, académica y de extensión tanto para estudiantes, docentes como personal administrativo.

#### 🎯 Objetivos generales del sistema:
- Servir como puerta de entrada institucional para los distintos actores vinculados con la Escuela.
- **Optimizar la comunicación interna** mediante anuncios actualizados y visibles desde el portal principal.
- **Ofrecer enlaces rápidos y organizados** a recursos clave en los ámbitos de docencia, investigación, acción social y vida estudiantil.

#### 👥 Tipos de usuarios:
- **Estudiantes**: acceden a noticias, calendario académico, horarios de cursos, bolsas de empleo y procesos de graduación.
- **Docentes**: consultan recursos institucionales, información de proyectos, actividades académicas y administrativas.
- **Administrativos**: gestionan el contenido publicado, estructuran la organización interna y actualizan la información crítica para la comunidad.

#### 🧩 Funcionalidades clave:
- **Anuncios destacados**: desde la portada se publican recordatorios y eventos como el calendario de graduaciones, convocatorias de Radio201, horarios de cursos y ferias de empleo.
- **Menú desplegable organizado** en cinco grandes áreas:
  - 📚 **Estudios**: plan de estudios, matrícula, programas académicos.
  - 🧪 **Investigación**: proyectos activos, grupos de investigación.
  - 🎓 **Docencia**: personal docente, guías, normativas.
  - 🧭 **Acción Social**: programas, iniciativas comunitarias.
  - 🏫 **Escuela**: historia, estructura organizacional, comisiones.

- **Integración de enlaces útiles**: como acceso a sistemas de matrícula, bibliotecas, reglamentos universitarios y recursos de apoyo.
- **Diseño responsivo y navegación intuitiva**, con secciones jerarquizadas que permiten al usuario llegar fácilmente a la información deseada.

En conjunto, EIEInfo actúa como un centro digital de operaciones que conecta a los miembros de la EIE con su vida institucional y académica, fortaleciendo los canales de información y el vínculo con la comunidad universitaria.

## Identificación de Tecnologías utilizadas
Basándose en la documentación y estructura general del proyecto, el sistema de EIE implementa varias tecnologías/servicios distintos para el *deployment/funcionamiento* de la página, al igual que para su *desarrollo y verificación*.

### 🔬 Desarrollo/verificación:

#### [Docker:](https://www.docker.com/)
- **Ambiente de desarrollo:** Crea un ambiente de desarrollo/prueba lo más parecido posible a la instancia real ejecutada en [Faraday](#faraday), permitiendo recrear el entorno de deployment para propósitos de desarrollo y depuración de cambios. El docker empleado por EIEInfo genera 3 contenedores para la [base de datos](#mariadb-base-de-datos), [NGINX](#nginx-reverse-proxy-servidor-de-archivos-estáticos-y-terminador-ssl) y el [Django](#django-framework-y-backend).

#### [Drone](https://drone.eie.ucr.ac.cr/welcome)
- **Pipeline CI/CD:** Se utiliza para la ejecución de pruebas y pipelines de integración y despliegue continuo (CI/CD). Se utiliza en conjunto con los contenedores de Docker.

#### [Flake8:](https://flake8.pycqa.org/en/latest/)
- **Formato:** Estándar con reglas de formato PEP8 que se deben seguir en los scripts de Python del proyecto, se pueden utilizar distintos linters para asegurar que se cumplan, y se usa un archivo .flake8 para especificar exclusiones en el proceso de revisión.

### 📲 Deployment/funcionamiento:

#### Faraday:
- **Hardware para hosting:** Es el servidor propio de la Escuela de Ingeniería Eléctrica (EIE), en el cual se ejecutan las herramientas principales para el despliegue de la página de eie.
- **Almacenamiento:** Almacena el backend del sitio, incluyendo todos los scripts/settings para el despliegue de la aplicación, al igual que la base de datos con la información de usuarios.

#### [NGINX ("Reverse proxy", servidor de archivos estáticos y terminador SSL):](https://nginx.org/)
- **Punto de entrada:** Es el servidor del front-end, y el primer punto de entrada al que llegan los requests de un usuario.
- **Terminal SSL/TLS:** Descifra o encripta los requests HTTP que entran/salen del sistema EIE, realizando el *handshake* de seguridad en capa de transporte (ya sea SSL o TLS).
- **Servicio de archivos estáticos:** Para requests estáticos, que requieren el despliegue de archivos estáticos (imágenes, formato de página, etc), NGINX los retorna directamente de forma eficiente sin tener que consultar a capas posteriores.
- **Reverse proxy:** Para requests dinámicos, que requieren consultar datos de la base de datos o procesamiento, se reenvían los requests al servidor Gunicorn por medio de un puerto interno en el hardware de Faraday.

#### [Gunicorn (Servidor WSGI HTTP):](https://gunicorn.org/)
- **WSGI (Web Server Gateway Interface):** Funciona como la interfaz entre el backend escrito en Python y los requests vistos por el servidor NGINX. Traduce los requests a un formato entendido por Python (WSGI standard) para el backend y las respuestas del backend a requests para el servidor NGINX.
- **Comunicación interna:** Se comunica con el servidor NGINX por medio de un puerto local o un socket dentro del hardware de Faraday, esto evita exponer el resto del sistema al internet abierto (más robusto).
- **Manejo de workers:** Se encarga de crear/manejar instancias de procesos "workers" que ejecutan el framework de Django, permitiendo el manejo de varios usuarios concurrentes. También mantiene la estabilidad en casos de fallo de un worker, puesto que se crea otra instancia de worker sin afectar al resto.

#### [Django (Framework y backend):](https://www.djangoproject.com/)
- **Framework:** Maneja la lógica interna de la página, incluyendo las interacciones con la base de datos y procesamiento de datos.
- **Templates:** Define y edita las vistas generadas en cada URL de la página, al igual que el formato de las páginas.

#### [MariaDB (Base de datos):](https://mariadb.org/)
- **Almacenamiento de datos persistente:** Almacena todos los datos de usuarios, de contenido (Django) y demás de forma persistente. Es modificada por medio del ORM de Django, según los modelos definidos en el framework. Se usa MariaDB, un fork de MySQL altamente compatible con el mismo.

La estructura del proyecto según estas herramientas se muestra en el siguiente diagrama:

```mermaid
graph TD
    subgraph Internet
        User_Browser[User's Web Browser]
    end

    subgraph Faraday_Server["**Faraday Server**<br>(IP: xxx.xxx.xxx.xxx)"]
        NGINX_SSL(NGINX:<br>Web Server / Proxy / SSL / Static)
        Gunicorn(Gunicorn:<br>WSGI HTTP Server)
        Django[Django:<br>Logic / ORM / Templates]
        Database[(Database:<br> MariaDB)]
    end

    User_Browser -- HTTPS Request --> NGINX_SSL

    NGINX_SSL -- Serve Static Files Directly<br>(if /static/ or /media/) --> User_Browser
    NGINX_SSL -- Forward Dynamic Request<br>(via local socket/port) --> Gunicorn

    Gunicorn -- WSGI Protocol --> Django

    Django -- ORM Queries --> Database
    Database -- Data Results --> Django

    Django -- HTML Response --> Gunicorn
    Gunicorn -- HTTP Response --> NGINX_SSL

    NGINX_SSL -- Encrypted HTTPS Response --> User_Browser

    %% Muted color styles for dark background
    style User_Browser fill:#5A9BD4,stroke:#222,stroke-width:1.5px,color:#fff
    style NGINX_SSL fill:#D88C4A,stroke:#222,stroke-width:1.5px,color:#fff
    style Gunicorn fill:#6FBF73,stroke:#222,stroke-width:1.5px,color:#fff
    style Django fill:#4A90E2,stroke:#222,stroke-width:1.5px,color:#fff
    style Database fill:#C94C4C,stroke:#222,stroke-width:1.5px,color:#fff
    style Faraday_Server fill:#2B2B2B,stroke:#aaa,stroke-width:1.5px,stroke-dasharray: 5 5,color:#fff
```

## Módulos Clave del Sistema
### `cursos/`
- Este módulo se encarga de todo lo relacionado con los cursos de la EIE: desde la gestión de materias y grupos, hasta la asignación de aulas y horarios. También permite emitir cartas a estudiantes y coordinar los horarios de consulta de los profesores y la asignación de cátedras.

### `trabajos_finales/`
- Aquí se administra todo el proceso de los trabajos finales de graduación. Permite gestionar proyectos de grado, asignar lectores y evaluadores, hacer seguimiento al avance de los estudiantes y organizar concursos relacionados con los trabajos finales.

### `proyecto_electrico/`
- Este módulo está dedicado a la gestión de los proyectos eléctricos desarrollados por estudiantes. Facilita el registro, control y seguimiento de los proyectos, así como la asignación de recursos, materiales y laboratorios necesarios para su desarrollo.

### `practica_profesional/`
- Permite administrar las prácticas profesionales de los estudiantes, registrando y dando seguimiento a cada práctica. Además, gestiona las empresas colaboradoras, los supervisores asignados y evalúa el desempeño y cumplimiento de objetivos de los estudiantes.

### `profesores/`
- Este módulo centraliza la gestión del personal docente, almacenando información personal y profesional, gestionando nombramientos y cargas académicas, administrando perfiles y documentación, y controlando la participación en comisiones y consejos.

### `estudiantes/`
- Se encarga de la administración de toda la comunidad estudiantil: registro, consulta y actualización de datos, control de matrículas y cargas académicas, seguimiento del historial y rendimiento académico, y la gestión de asignaciones a grupos, carreras o proyectos.

### `administrativos/`
- Este modulo gestiona el personal administrativo, permitiendo registrar funciones por puesto, controlar las responsabilidades de cada funcionario y administrar recursos y documentación de soporte.

### `alumni/`
- Este módulo permite mantiener un vínculo con los egresados de la EIE, actualizando sus datos, siguiendo su trayectoria profesional y promoviendo redes de contacto y colaboración con la comunidad.

### `anuncios/`
- Gestiona las comunicaciones internas de la escuela, permitiendo publicar anuncios oficiales, segmentar la información por perfiles de usuario y controlar la edición, eliminación y auditoría de los anuncios.

### `eventos/`
- Módulo para organizar y administrar los eventos académicos y administrativos, gestionando la programación, los calendarios compartidos y los recursos logísticos necesarios para cada evento.

### `conferencias/`
- Este módulo se enfoca en la organización de conferencias y seminarios especializados, registrando ponentes y asistentes, controlando la logística y generando certificados de participación.

### `laboratorios/`
- Este módulo gestiona el uso y mantenimiento de los laboratorios, registrando equipos y materiales disponibles, organizando horarios de uso y controlando los mantenimientos programados y correctivos.

### `inventario/`
- Este módulo permite administrar el inventario físico de la escuela, llevando un control detallado de recursos, herramientas y activos, registrando entradas y salidas, y gestionando los préstamos temporales.

### `proyectos/`
- Gestiona los proyectos de investigación vinculados a la escuela, registrando y documentando los proyectos activos, controlando recursos y haciendo seguimiento de hitos y resultados.

### `asistencias/`
- Este módulo controla la asistencia en actividades, ya sea de forma automática o manual, gestionando horarios y generando reportes y análisis de participación.

### `atributos/`
- Permite configurar los atributos técnicos del sistema, gestionando parámetros, etiquetas y características, y personalizando funcionalidades mediante atributos configurables.

### `webpage/`
- Administra el sitio web oficial de la EIE, gestionando el contenido institucional, noticias y enlaces, controlando accesos y permisos de edición, e integrando otros módulos del sistema.

### `eieinfo/`
- Es donde se controlan los parámetros globales, las integraciones externas y la configuración de autenticación, rutas y roles.

### `scripts/`
- Almacena scripts utilitarios para tareas recurrentes, automatizando procesos administrativos o técnicos y facilitando el mantenimiento, respaldo y limpieza de datos.