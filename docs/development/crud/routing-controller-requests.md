# Rutas, controller y FormRequest

!!! info "Ficha documental"
    - Estado: `vigente`
    - Tipo: `how-to`
    - Audiencia: desarrolladores que implementan el backend HTTP de módulos CRUD
    - Fuente verificable: `routes/`, `app/Http/Controllers/`, `app/Http/Requests/`, `app/Policies/` y [ADR-009](../../adr/ADR-009-crud-module-standard.md)

El backend CRUD mantiene una ruta por módulo, controllers explícitos y FormRequests para toda mutación.

## Route file del módulo

```php
<?php

use App\Http\Controllers\{Module}\{Model}Controller;
use Illuminate\Support\Facades\Route;

Route::middleware(['auth', 'verified', 'ensure-two-factor'])
    ->prefix('{module}')
    ->name('{module}.')
    ->group(function () {
        Route::resource('{resource}', {Model}Controller::class)
            ->only(['index', 'create', 'store', 'show', 'edit', 'update', 'destroy']);
    });
```

Registra el archivo al final de `routes/web.php`:

```php
require __DIR__.'/{module}.php';
```

## Nombres de ruta

| Acción | Nombre |
| --- | --- |
| Index | `{module}.{resource}.index` |
| Create | `{module}.{resource}.create` |
| Store | `{module}.{resource}.store` |
| Show | `{module}.{resource}.show` |
| Edit | `{module}.{resource}.edit` |
| Update | `{module}.{resource}.update` |
| Destroy | `{module}.{resource}.destroy` |
| Restore | `{module}.{resource}.restore` |
| Force delete | `{module}.{resource}.force-delete` |

## Controller

```php
<?php

namespace App\Http\Controllers\{Module};

use App\Http\Controllers\Controller;
use App\Http\Requests\{Module}\Store{Model}Request;
use App\Http\Requests\{Module}\Update{Model}Request;
use App\Models\{Model};
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Gate;
use Inertia\Inertia;
use Inertia\Response;

class {Model}Controller extends Controller
{
    public function index(Request $request): Response
    {
        Gate::authorize('viewAny', {Model}::class);

        $models = {Model}::query()
            ->when($request->search, fn ($query, $search) => $query->where('name', 'ilike', "%{$search}%"))
            ->latest()
            ->paginate(15)
            ->withQueryString();

        return Inertia::render('{module}/{resource}/index', [
            'models' => $models,
            'filters' => $request->only(['search']),
            'breadcrumbs' => [
                ['title' => '{Recursos}'],
            ],
        ]);
    }

    public function store(Store{Model}Request $request): RedirectResponse
    {
        {Model}::create($request->validated());

        return to_route('{module}.{resource}.index')
            ->with('success', '{Recurso} creado exitosamente.');
    }

    public function update(Update{Model}Request $request, {Model} $model): RedirectResponse
    {
        $model->update($request->validated());

        return to_route('{module}.{resource}.index')
            ->with('success', '{Recurso} actualizado exitosamente.');
    }

    public function destroy({Model} $model): RedirectResponse
    {
        Gate::authorize('delete', $model);

        $model->delete();

        return to_route('{module}.{resource}.index')
            ->with('success', '{Recurso} eliminado exitosamente.');
    }
}
```

## Reglas de controller

- Usa `Gate::authorize()` en cada acción.
- Usa `ilike` para búsquedas PostgreSQL case-insensitive.
- Conserva filtros en paginación con `->withQueryString()`.
- Flashea mensajes con `success`, `error`, `info` o `warning`; `HandleInertiaRequests` los comparte y `FlashToaster` los muestra.
- En creación contextual, autoriza el padre y también la creación del recurso hijo.

## FormRequests

```php
<?php

namespace App\Http\Requests\{Module};

use App\Models\{Model};
use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Support\Facades\Gate;

class Store{Model}Request extends FormRequest
{
    public function authorize(): bool
    {
        return Gate::allows('create', {Model}::class);
    }

    /** @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array<mixed>|string> */
    public function rules(): array
    {
        return [
            'name' => ['required', 'string', 'max:255'],
        ];
    }
}
```

```php
<?php

namespace App\Http\Requests\{Module};

use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Support\Facades\Gate;

class Update{Model}Request extends FormRequest
{
    public function authorize(): bool
    {
        return Gate::allows('update', $this->route('{model}'));
    }

    /** @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array<mixed>|string> */
    public function rules(): array
    {
        return [
            'name' => ['required', 'string', 'max:255'],
        ];
    }
}
```

`authorize()` es la capa 3 del modelo de seguridad y se ejecuta antes de `rules()`. Para store se autoriza contra la clase; para update se autoriza contra la instancia route-bound.
