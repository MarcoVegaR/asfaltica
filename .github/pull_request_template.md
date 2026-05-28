## Resumen

- 

## Validación

- [ ] Tests o comandos relevantes ejecutados.
- [ ] `mkdocs build --strict` ejecutado si el cambio toca documentación o navegación documental.
- [ ] El workflow `docs` debe pasar si el cambio toca `docs/`, `mkdocs.yml` o `requirements.txt`.

## Checklist documental

- [ ] Declaré impacto documental: no aplica, README, `docs/`, ADR, referencia derivable/generada o PRD/gobernanza.
- [ ] Actualicé `docs/` o ADRs si el cambio modifica comportamiento, arquitectura, operación o comandos relevantes.
- [ ] No dupliqué catálogos que pueden derivarse con comandos como `php artisan route:list`, `php artisan list` o `php artisan config:show`.
- [ ] El estado documental sigue claro: vigente, histórico, reemplazado, borrador o deprecated.
- [ ] Si agregué o cambié una decisión arquitectónica, actualicé un ADR con estado proposed, accepted, superseded o rejected.
