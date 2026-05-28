# Primeros pasos

!!! info "Ficha documental"
    - Estado: `vigente`
    - Tipo: `tutorial`
    - Audiencia: personas que levantan el proyecto localmente
    - Fuente verificable: `README.md`, `.env.example`, `composer.json`, `package.json` y `mkdocs.yml`

Usa el `README.md` como quickstart operativo del repositorio. Este sitio amplía ese punto de entrada con documentación técnica curada.

!!! abstract "Objetivo"
    Dejar el proyecto instalado, migrado y servido localmente con la mínima cantidad de pasos verificables.

## Flujo local mínimo

```bash
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan migrate
composer run dev
```

Para validar la documentación:

```bash
python -m pip install -r requirements.txt
mkdocs build --strict
```

!!! tip "Vista local"
    Para revisar el sitio antes de publicar, ejecuta `mkdocs serve` y abre la URL local que indique la consola.
