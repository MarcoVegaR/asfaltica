# Boilerplate Laravel 13

Boilerplate local para Laravel 13 basado en el starter oficial de React, con Inertia, Fortify, Wayfinder, PostgreSQL, Redis, Mailpit, MinIO y Laravel AI SDK.

La documentación técnica publicada vive en GitHub Pages: <https://marcovegar.github.io/boilerplate-laravel13/>.

## Stack principal

- Laravel 13
- React 19 + Inertia v2
- Tailwind CSS v4
- PostgreSQL
- Redis
- Mailpit
- MinIO
- Laravel Boost + Laravel AI SDK + flujos del ecosistema Gentleman

## Nota del starter

El proyecto parte de `laravel/react-starter-kit` y ya incluye autenticación con Fortify más páginas React renderizadas con Inertia.

## Servicios locales

La línea base local esperada es:

- PostgreSQL en `127.0.0.1:5432`
- Redis en `127.0.0.1:6379`
- Mailpit SMTP en `127.0.0.1:1025`
- UI web de Mailpit en `http://127.0.0.1:8025`
- API S3 de MinIO en `http://127.0.0.1:9000`
- Consola de MinIO en `http://127.0.0.1:9001`

Los valores por defecto del entorno están preparados para:

- idioma: `es` con fallback `en`
- faker locale: `es_VE`
- zona horaria: `America/Caracas`
- cache/sesiones/colas: Redis
- almacenamiento de objetos: MinIO mediante el disco Laravel `s3`

## Instalación inicial

1. Instala dependencias PHP y Node:

```bash
composer install
npm install
```

2. Prepara el archivo de entorno:

```bash
cp .env.example .env
php artisan key:generate
```

3. Asegura que PostgreSQL, Redis, Mailpit y MinIO estén corriendo.

4. Ejecuta las migraciones:

```bash
php artisan migrate
```

5. Inicia la aplicación:

```bash
composer run dev
```

Este comando ejecuta juntos el servidor Laravel, el listener de colas, el seguimiento de logs y Vite.

Para procesos locales dedicados:

```bash
composer run local:queue
composer run local:schedule
```

## Comandos diarios

```bash
composer run dev
composer run local:queue
composer run local:schedule
php artisan test --compact
vendor/bin/pint --dirty --format agent
npm run build
mkdocs build --strict
```

Usa `npm run build` para compilar assets de producción. Usa `npm run dev` si solo necesitas Vite.

## Documentación

La documentación técnica vive en `docs/` y se sirve con MkDocs Material. Este README es el quickstart principal; usa el sitio publicado para arquitectura, desarrollo, operaciones, referencia y ADRs curados.

Sitio publicado: <https://marcovegar.github.io/boilerplate-laravel13/>.

Instala las dependencias fijadas de documentación y valida el sitio con:

```bash
python -m pip install -r requirements.txt
mkdocs build --strict
```

GitHub Actions valida documentación en pull requests y publica GitHub Pages desde `main`.

## Mailpit

El correo está configurado para Mailpit vía SMTP:

- `MAIL_MAILER=smtp`
- `MAIL_HOST=127.0.0.1`
- `MAIL_PORT=1025`

Abre la bandeja en `http://127.0.0.1:8025`.

## Redis

Redis es el servicio local por defecto para:

- cache
- sesiones
- colas

Esto acerca el desarrollo local a un runtime estilo Laravel Cloud sin asumir infraestructura cloud real.

## MinIO

El almacenamiento local de objetos usa el disco Laravel `s3` y apunta a MinIO por defecto:

- endpoint: `http://127.0.0.1:9000`
- consola: `http://127.0.0.1:9001`
- bucket: `boilerplate-laravel13-local`

Las credenciales locales de MinIO se definen en `.env` con `MINIO_ROOT_USER` y `MINIO_ROOT_PASSWORD`, y luego se reutilizan mediante las variables `AWS_*` esperadas por Laravel.

## Laravel AI SDK

El Laravel AI SDK oficial está instalado y publicado.

- Paquete: `laravel/ai`
- Configuración: `config/ai.php`
- Tablas de conversación: publicadas y migradas

Añade en `.env` la clave del proveedor que quieras usar, por ejemplo:

- `OPENAI_API_KEY`
- `GEMINI_API_KEY`
- `ANTHROPIC_API_KEY`
- `OLLAMA_BASE_URL` para uso local con Ollama

La configuración AI por defecto apunta generación de texto a OpenAI y generación de imágenes a Gemini hasta que elijas otro proveedor.

## Tooling AI en este repositorio

- Laravel Boost está disponible para documentación contextual, logs, inspección de base de datos y tooling del framework.
- Laravel AI SDK está disponible para agentes de aplicación, tools, embeddings y almacenamiento conversacional.
- La coordinación del ecosistema Gentleman está documentada en `AGENTS.md` para memoria, SDD y prácticas human-in-the-loop.

## Verificación

Checks enfocados útiles:

```bash
php artisan test --compact tests/Feature/ExampleTest.php tests/Feature/DashboardTest.php tests/Feature/Auth/AuthenticationTest.php
php artisan config:show filesystems.disks.s3
php artisan tinker --execute="dump(Storage::disk('s3')->allFiles())"
vendor/bin/pint --dirty --format agent
php artisan config:show app
```

## English Summary

This repository is a Laravel 13 + Inertia React boilerplate. Start with the setup commands above, then use the published documentation at <https://marcovegar.github.io/boilerplate-laravel13/> for architecture, development, operations, references, and ADRs.

## Notas

- Si los cambios frontend no se ven, ejecuta `npm run build`, `npm run dev` o `composer run dev`.
- Si Redis, Mailpit o MinIO no están corriendo, colas, sesiones, cache, correo o almacenamiento de objetos fallarán de forma esperada hasta que esos servicios locales estén disponibles.
