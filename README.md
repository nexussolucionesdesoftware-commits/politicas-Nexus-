# README

# Política de Control de Cambios de Software

**Nexus Soluciones de Software**

**v. 0.1.0-borrador**

- **Fecha de Creación:** 26 de abril de 2026
- **Última Actualización:** 26 de abril de 2026
- **Próxima Revisión:** 
- **Elaborado por:** Nexus Soluciones de Software

## Objetivo

Esta política establece cómo **Nexus Soluciones de Software** debe manejar los cambios en el software desarrollado para sus clientes, de forma segura, controlada y documentada. Siguiendo estándares como **ISO 27001** e **ITIL**, se busca proteger la seguridad de la información, garantizar la calidad del servicio prestado y asegurar que los cambios se realicen minimizando el riesgo de interrumpir los sistemas de los clientes contratantes.

## Alcance

Aplica a **todos los proyectos de software desarrollados por Nexus Soluciones de Software** para sus empresas clientes, incluyendo aplicaciones web, móviles, de escritorio, bases de datos y APIs, independientemente del sector o tamaño de la empresa contratante. Es obligatoria para todo el personal de Nexus involucrado en el desarrollo, mantenimiento y operación de los sistemas de información, así como para los representantes del cliente que participen en el proceso de aprobación de cambios.

## Definiciones

- **Cambio:** Modificación en el código, configuración o infraestructura de software.  
- **Cliente:** Empresa que contrata los servicios de desarrollo de software de Nexus Soluciones de Software.  
- **Representante del Cliente:** Persona designada por la empresa cliente como punto de contacto y aprobación de cambios.  
- **Ventana de Mantenimiento:** Periodo programado para realizar cambios con el menor impacto posible.  
- **Versionamiento Semántico (SemVer):** Método de asignación de versiones basado en [**MAJOR.MINOR.PATCH**](https://semver.org/lang/es/).  
- **Ambiente de Producción del Cliente:** Entorno donde opera el sistema en uso real por parte de la empresa contratante.  

## Pasos para el Control de Cambios

### 1. Versionamiento de Código en Git (por el Desarrollador)

- Antes de iniciar cualquier proceso de publicación, el desarrollador debe versionar sus cambios en la herramienta de versionamiento institucional, asegurando que todas las modificaciones estén documentadas y listas para revisión.
- Este versionamiento sirve para llevar el control de cambios internos durante el desarrollo y asegurar que cada cambio esté registrado.

### 2. Documentación y Creación de Ticket

- El desarrollador genera un ticket en el sistema de gestión de cambios, proporcionando una descripción detallada de los cambios y los pasos necesarios para publicar. El ticket debe indicar el **cliente al que pertenece el proyecto**. Esto incluye:
  - Scripts SQL (DDL, DML, DCL) para bases de datos.
  - Creación o modificación de permisos o roles.
  - Instrucciones claras para la publicación del software.
  - Impacto esperado en el cliente y sus usuarios finales.

### 3. Aprobación del Cliente

- Antes de proceder con la publicación, el **Gestor de Cambios** de Nexus debe presentar el resumen del cambio al **Representante del Cliente** para su aprobación formal, ya sea por escrito (correo electrónico, plataforma de gestión) o mediante acta de reunión.
- Para cambios de tipo **MAJOR** o que afecten funcionalidades críticas del cliente, la aprobación escrita es obligatoria.
- Una vez obtenida la aprobación, el desarrollador convoca una reunión interna con los responsables de base de datos y servidores para coordinar el impacto técnico.
- En la reunión se aclaran dudas y se ajustan los detalles necesarios para proceder con la publicación.

### 4. Preparación de la Publicación en Producción

- **Versionamiento Final en la Rama de Producción (por el Encargado de Producción):** El encargado de producción se encarga de aplicar una “release” en la rama de producción, verificando que los cambios están controlados y listos para el despliegue final.

### 5. Programación en la Ventana de Mantenimiento

- Se programa la publicación en horarios de baja carga (ventana de mantenimiento), acordados previamente con el cliente, para minimizar el impacto en su operación.
- Si la publicación requiere una interrupción del servicio, el encargado de producción debe notificar al **Representante del Cliente** con la debida anticipación y coordinar con el equipo de soporte de Nexus.

### 6. Publicación y Documentación Final

- El encargado de producción realiza la publicación en el entorno de producción del cliente.
- Se documenta todo el proceso en el ticket, dejando un registro detallado de cada paso y resultado de la publicación.
- Al finalizar, se notifica al **Representante del Cliente** y a los interesados internos de Nexus sobre los cambios implementados, adjuntando el resumen del ticket como evidencia del proceso.

## Buenas Prácticas para Commits en Git

Todo el equipo de desarrollo de Nexus debe seguir estas reglas al registrar cambios en Git, para mantener un historial limpio, legible y trazable en todos los proyectos.

### 1. Usa el verbo imperativo en el mensaje

Escribe el mensaje como una instrucción que describe qué hace el commit al aplicarse. Verbos recomendados: `Add`, `Change`, `Fix`, `Remove`, `Update`, `Refactor`.

> Si aplico este commit, entonces este commit… *Add new login validation*

### 2. No uses punto final ni puntos suspensivos

El título del commit no lleva puntuación al final. Cada carácter cuenta: sé directo y conciso.

- ❌ `Fix a problem with the login form.`
- ✅ `Fix a problem with the login form`

### 3. Máximo 50 caracteres en el título

Si el mensaje es muy largo, es señal de que el commit hace demasiadas cosas. Divide los cambios en commits más pequeños y atómicos.

### 4. Añade contexto en el cuerpo del mensaje cuando sea necesario

Cuando el cambio requiere explicación adicional (motivo, impacto, decisión técnica), agrégala en el cuerpo del commit separado del título por una línea en blanco. El cuerpo sí puede usar puntuación normal.

### 5. Usa prefijos semánticos (Conventional Commits)

Todo commit en Nexus debe iniciar con un prefijo que indique el tipo de cambio, siguiendo el estándar [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/):

```
<tipo>[scope opcional]: <descripción>
```

| Prefijo | Cuándo usarlo |
|---|---|
| `feat` | Nueva funcionalidad para el usuario |
| `fix` | Corrección de un bug que afecta al usuario |
| `docs` | Cambios en documentación |
| `style` | Formato, espacios, puntos y coma (sin impacto funcional) |
| `refactor` | Reestructuración del código sin cambiar comportamiento |
| `test` | Añade o modifica pruebas |
| `build` | Cambios en el sistema de build o dependencias |
| `ci` | Cambios en integración continua |
| `perf` | Mejoras de rendimiento |

Ejemplos:

- `feat: add password recovery flow`
- `fix: correct tax calculation on invoice`
- `docs: update README with deployment steps`

Para proyectos con múltiples módulos, se puede agregar el scope:

- `feat(api): add endpoint for user reports`
- `fix(web): remove broken pagination`

### 6. Referencia el ticket o issue en el commit

Siempre que exista un ticket en el sistema de gestión de cambios, debe referenciarse en el mensaje del commit. Esto vincula el código con la tarea que lo motivó.

- Para referenciar sin cerrar: `feat: add report export #45`
- Para cerrar automáticamente (en GitHub/GitLab): `fix: correct date format closes #45`

### 7. Usa herramientas para garantizar el estándar

Se recomienda configurar en los repositorios de Nexus las siguientes herramientas:

- **commitlint**: valida que cada commit siga el formato de prefijos semánticos antes de ser registrado.
- **husky**: ejecuta hooks de Git (por ejemplo, correr tests antes del push).
- **commitizen**: guía interactiva por línea de comandos para construir commits bien formados.

---

## Recomendación para el Versionamiento del Componente

Cada proyecto entregado por Nexus debe tener una versión asignada siguiendo el esquema de [**Versionamiento Semántico (SemVer)**](https://semver.org/lang/es/):

```
MAJOR . MINOR . PATCH
  1   .   0   .   1
```

| Segmento | Qué representa | Cuándo se incrementa |
|---|---|---|
| **MAJOR** | Versión principal | Cambios que rompen compatibilidad con versiones anteriores (rediseño de módulos, cambios en la estructura de BD, migraciones obligatorias) |
| **MINOR** | Funcionalidad nueva | Nueva característica compatible con la versión actual (nuevo módulo, nuevo endpoint, nueva pantalla) |
| **PATCH** | Corrección | Bugfix, ajuste menor, cambio de texto o configuración sin nuevas funciones |

**Ejemplos prácticos:**

- `1.0.0` → Primer lanzamiento estable a producción
- `1.0.1` → Se corrigió un bug en el módulo de facturación
- `1.1.0` → Se agregó el módulo de reportes
- `2.0.0` → Se rediseñó el sistema de autenticación (cambio incompatible con v1)

**Versión inicial:** Todo proyecto nuevo inicia en `0.1.0` durante la fase de desarrollo. El primer despliegue formal a producción acordado con el cliente se libera como `1.0.0`.

**Relación entre tipo de commit y versión:**

Los prefijos semánticos de los commits determinan directamente qué segmento de la versión se incrementa al generar una nueva release:

| Tipo de commit | Efecto en la versión | Ejemplo |
|---|---|---|
| `fix` | Incrementa **PATCH** | `1.0.0` → `1.0.1` |
| `feat` | Incrementa **MINOR** | `1.0.1` → `1.1.0` |
| `feat` + `BREAKING CHANGE` | Incrementa **MAJOR** | `1.1.0` → `2.0.0` |

La versión debe reflejarse en la documentación del proyecto (`README.md` o `CHANGELOG.md`) antes de su aprobación final para producción.

## Control de Versiones y Auditoría

Cada versión publicada debe contar con un identificador único que siga el esquema de [**SemVer**](https://semver.org/lang/es/) y estar registrada tanto en el repositorio de versionamiento como en la documentación del proyecto. El sistema de tickets debe contener una descripción detallada del cambio y un registro de todas las acciones realizadas en producción.

## Roles y Responsabilidades

- **Desarrollador (Nexus):** Documenta el cambio, versiona el código, crea el ticket y proporciona instrucciones detalladas para la publicación.
- **Encargado de Producción (Nexus):** Revisa los cambios, aplica la versión de release en producción y asegura que todo esté registrado y documentado en el sistema de tickets.
- **Gestor de Cambios (Nexus):** Coordina los cambios entre el equipo técnico y el cliente, gestiona la aprobación y verifica el cumplimiento de esta política.
- **Representante del Cliente:** Aprueba los cambios antes de su publicación, define las ventanas de mantenimiento aceptables y recibe la notificación de los resultados. No tiene acceso directo a los entornos de Nexus, pero debe ser informado en cada etapa relevante.

## Cumplimiento y Auditoría

- **Revisión Periódica:** Esta política se revisará semestralmente para asegurar su alineación con las mejores prácticas y estándares, y podrá ser ajustada según los acuerdos de nivel de servicio (SLA) vigentes con los clientes.  
- **Auditorías:** Se realizarán auditorías regulares para verificar que cada etapa se haya cumplido adecuadamente. Los registros podrán ser puestos a disposición del cliente ante solicitud formal.  
- **Incumplimiento:** Cualquier incumplimiento por parte del equipo de Nexus será reportado a la dirección de la empresa para las acciones correctivas correspondientes. Los clientes serán notificados si el incumplimiento afecta directamente el servicio contratado.

## Sustento en ISO 27001 e ITIL

1. **ISO 27001:** Asegura que los cambios se gestionan de forma segura, protegiendo la integridad de los sistemas y evitando modificaciones no autorizadas que puedan afectar la seguridad.
2. **ITIL:** Proporciona un marco de buenas prácticas para la gestión de servicios de TI, que incluye:
   - Procesos claros de evaluación, aprobación y comunicación de cambios.
   - Definición de roles y responsabilidades para un despliegue ordenado.

La combinación de estos estándares permite a **Nexus Soluciones de Software** garantizar a sus clientes que cada cambio en sus sistemas estará controlado, documentado y será seguro para sus entornos de producción, protegiendo tanto la información del cliente como la continuidad de su operación.

