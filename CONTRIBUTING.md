# Guía de contribución — Kintsugi Tattoo

## 1. Objetivo

Establecer reglas de colaboración para el desarrollo de Kintsugi Tattoo, manteniendo la calidad del código, la trazabilidad con Azure DevOps y la integridad del historial Git.

GitHub es el repositorio principal. Azure Repos mantiene una copia sincronizada de `main` mediante Azure Pipelines.

## 2. Estrategia de ramas

| Rama | Propósito | Destino del Pull Request |
|---|---|---|
| `main` | Código estable y aprobado | — |
| `dev` | Integración de funcionalidades | `main` |
| `feat/*` | Nuevas funcionalidades | `dev` |
| `fix/*` | Corrección de errores | `dev` |
| `hotfix/*` | Correcciones urgentes | `main` |
| `docs/*` | Documentación | `dev` |
| `chore/*` | Mantenimiento y configuración | `dev` |
| `ci/*` | Automatización y Pipelines | `dev` |
| `test/*` | Pruebas automatizadas | `dev` |
| `release/*` | Preparación de entregas | Según el plan de liberación |

Las ramas temporales se crean únicamente cuando comienza el trabajo correspondiente.

## 3. Nomenclatura

Utilizar minúsculas, guiones y nombres descriptivos, sin espacios, acentos ni caracteres especiales.

Formato recomendado para funcionalidades:

`feat/pbi-019-agendar-cita`

El código PBI debe corresponder al identificador utilizado en la planificación del proyecto.

Ejemplos adicionales:

- `fix/pbi-019-validacion-fecha`
- `docs/arquitectura`
- `ci/validacion-pr`
- `hotfix/error-autenticacion`

## 4. Convención de commits

Utilizar Conventional Commits:

`tipo(alcance): descripción`

Tipos aceptados: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build` y `perf`.

Ejemplos:

- `feat(citas): implementar registro de citas AB#245`
- `fix(auth): corregir validación de credenciales AB#246`
- `docs(api): documentar endpoints de clientes`
- `ci(pipeline): agregar validaciones automáticas`

Cuando exista un Work Item relacionado, utilizar su ID numérico real mediante `AB#ID`.

## 5. Flujo de desarrollo

1. Actualizar la rama `dev` local.
2. Crear una rama temporal a partir de `dev`.
3. Implementar los cambios correspondientes.
4. Realizar commits descriptivos.
5. Publicar la rama en GitHub.
6. Abrir un Pull Request hacia `dev`.
7. Documentar cambios, pruebas y Work Items relacionados.
8. Obtener la aprobación requerida.
9. Resolver las conversaciones pendientes.
10. Integrar los cambios y eliminar la rama temporal cuando ya no sea necesaria.

No se permiten pushes directos a `main` ni `dev`.

## 6. Pull Requests

Cada PR debe incluir:

- Resumen de los cambios.
- PBI y Work Items de Azure Boards relacionados, cuando existan.
- Descripción de las pruebas realizadas.
- Evidencias cuando sean aplicables.
- Consideraciones sobre dependencias o cambios incompatibles.

El PR debe recibir al menos una aprobación de un colaborador elegible y tener resueltas las conversaciones de revisión.

Se recomienda utilizar **Create a merge commit** para las integraciones de `dev` hacia `main`, conservando explícitamente el historial de integración.

## 7. Integración con Azure Repos

Azure Pipelines sincroniza automáticamente los cambios de `main` en GitHub hacia `main` en Azure Repos.

La sincronización es unidireccional.

No realizar modificaciones directas en Azure Repos `main`, porque podrían provocar divergencias y detener la Pipeline.

Las ramas `dev`, `uat` y `prod` de Azure Repos no forman parte de esta sincronización automática.

## 8. Correcciones urgentes

Los hotfixes se crean a partir de `main`, se revisan mediante Pull Request y, después de integrarse, deben incorporarse también en `dev`.

## 9. Seguridad y calidad

- No publicar contraseñas, tokens, archivos `.env` con secretos ni credenciales.
- No utilizar force push sobre `main` o `dev`.
- No eliminar ramas protegidas.
- No subir archivos generados, dependencias o configuraciones locales innecesarias.
- Ejecutar las pruebas disponibles antes de solicitar revisión.
- No modificar las reglas de protección para evitar una revisión.

## 10. Gestión del trabajo

Azure Boards es la fuente de seguimiento para épicas, PBIs y tareas del proyecto.

Las ramas representan unidades de desarrollo, no necesariamente tareas individuales. Los PR permiten relacionar el código entregado con el trabajo planificado.
