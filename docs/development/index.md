# Desarrollo

Estado: vigente

Este índice reúne guías para construir y verificar cambios dentro del boilerplate sin romper sus convenciones.

!!! tip "Regla práctica"
    Antes de crear una abstracción transversal, busca al menos tres casos reales que prueben la misma necesidad.

<div class="grid cards" markdown>

-   :material-rocket-launch-outline: **Primeros pasos**

    Flujo local mínimo para instalar, migrar y correr el proyecto.

    [Empezar](../getting-started.md)

-   :material-view-dashboard-edit-outline: **Módulos CRUD**

    Contrato operativo para pantallas, FormRequests, policies, rutas y pruebas.

    [Leer guía CRUD](../crud-module-guide.md)

</div>

## Referencias derivables

Prefiere comandos verificables frente a listas manuales:

- `php artisan list`
- `php artisan route:list`
- `php artisan test --compact`
- `vendor/bin/pint --dirty --format agent`
- `npm run build`
