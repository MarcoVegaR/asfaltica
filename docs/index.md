# Documentación técnica

Documentación técnica curada del boilerplate Laravel/Inertia. Este portal organiza arquitectura, desarrollo, operación, referencias y decisiones para que el proyecto pueda crecer sin deuda documental.

<div class="grid cards" markdown>

-   :material-rocket-launch-outline: **Primeros pasos**

    Levanta el entorno local, instala dependencias y valida que el proyecto responde.

    [Ir a primeros pasos](getting-started.md)

-   :material-sitemap-outline: **Arquitectura**

    Entiende las capas principales, límites técnicos y decisiones que gobiernan el boilerplate.

    [Ver arquitectura](architecture/index.md)

-   :material-code-braces: **Desarrollo**

    Convenciones para construir módulos, mantener consistencia y evitar bifurcaciones innecesarias.

    [Ver desarrollo](development/index.md)

-   :material-cog-outline: **Operaciones**

    Servicios locales, colas, scheduler, logging, auditoría y despliegue.

    [Ver operaciones](operations/index.md)

-   :material-book-open-page-variant-outline: **Referencia**

    Consultas curadas y fuentes derivables que no deben mantenerse como catálogos manuales.

    [Ver referencia](reference/index.md)

-   :material-file-sign-outline: **ADRs**

    Registro de decisiones arquitectónicas, estados y consecuencias.

    [Ver ADRs](adr/index.md)

</div>

!!! warning "Fuente de verdad"
    `docs/` es una capa de lectura técnica curada. Las fuentes verificables siguen siendo el código, tests, configuración, seeders, comandos ejecutables y ADRs vigentes.

!!! info "Publicación"
    El sitio está preparado para GitHub Pages en `https://marcovegar.github.io/boilerplate-laravel13/`. La publicación se valida con `mkdocs build --strict` antes del despliegue.

## Gobernanza documental

- No se mantienen catálogos completos manuales cuando pueden obtenerse por comando o inspección automatizada.
- Cada documento debe indicar o conservar su estado cuando su vigencia no sea obvia.
- Todo PR relevante debe declarar impacto documental en el checklist de revisión.
- Los documentos existentes se conservan en su ubicación actual hasta clasificarlos explícitamente por propósito y estado.

## Estados

=== "Documentos"

    - `vigente`: recomendado para trabajo actual.
    - `histórico`: se conserva para contexto, pero no guía trabajo nuevo.
    - `reemplazado`: sustituido por otro documento o ADR.
    - `borrador`: aún no aprobado como guía estable.
    - `deprecated`: sigue existiendo por compatibilidad, pero no debe ampliarse.

=== "ADRs"

    - `proposed`: decisión en discusión.
    - `accepted`: decisión vigente.
    - `superseded`: reemplazada por otro ADR.
    - `rejected`: decisión descartada.

## Referencias derivables

Estas referencias no deben mantenerse como catálogos manuales completos:

| Referencia | Fuente verificable |
| --- | --- |
| Rutas | `php artisan route:list` |
| Comandos Artisan | `php artisan list` y `php artisan help <comando>` |
| Variables de entorno propias | `.env.example`, `config/`, `php artisan config:show` |
| Permisos y roles | seeders, policies, middleware y tests de autorización |
| Jobs, listeners y eventos | `app/Jobs`, `app/Listeners`, `app/Events` y configuración relacionada |

## Inventario inicial

- Guías técnicas existentes: `authorization.md`, `crud-module-guide.md`, `operability-guide.md`.
- ADRs existentes: `adr/ADR-005-audit-boundary.md`, `adr/ADR-007-logging-and-correlation.md`, `adr/ADR-008-queue-and-scheduler-policy.md`, `adr/ADR-009-crud-module-standard.md`, `adr/ADR-011-copilot-backend-audit.md`.
- PRDs en raíz: `PRD-*.md`; se tratan como producto/historia/gobernanza hasta clasificarlos.
- Ayuda de usuario: `resources/help/**/*.md`; no forma parte de la documentación técnica MkDocs.

## Validación

```bash
mkdocs build --strict
```
