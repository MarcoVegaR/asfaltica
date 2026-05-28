# Operaciones

Estado: vigente

Este índice enlaza prácticas operativas para ejecutar, observar y mantener el proyecto en entornos locales y de despliegue.

!!! warning "No duplicar configuración"
    Las variables y servicios se explican por intención. Los valores verificables viven en `.env.example`, `config/` y workflows.

<div class="grid cards" markdown>

-   :material-console-line: **Operabilidad**

    Servicios locales, logs, colas, scheduler y verificación operativa.

    [Leer guía de operabilidad](../operability-guide.md)

-   :material-github: **GitHub Pages**

    La documentación se construye con `mkdocs build --strict` y se publica desde GitHub Actions.

    [Ver workflow](https://github.com/MarcoVegaR/boilerplate-laravel13/actions)

</div>

## Fuentes verificables

- Configuración en `config/`.
- Variables locales documentadas en `.env.example`.
- Comandos disponibles con `php artisan list`.
- Jobs, listeners y eventos presentes en `app/`.
