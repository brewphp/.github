<!-- Logo placeholder: replace this heading with the BrewPHP logo once it exists. -->
<h1 align="center">☕ BrewPHP</h1>

<p align="center"><strong>A small, Django-inspired PHP framework: easy to learn, with a readable core and no runtime dependencies.</strong></p>

<p align="center">
  <a href="https://github.com/brewphp/brewphp/blob/main/LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-6F4E37.svg"></a>
  <img alt="PHP >= 8.2" src="https://img.shields.io/badge/php-%3E%3D8.2-C8A27A.svg">
  <a href="https://docs.brewphp.dev"><img alt="Documentation" src="https://img.shields.io/badge/docs-docs.brewphp.dev-6F4E37.svg"></a>
  <!-- CI and coverage badges will be added once the GitHub Actions workflows exist. -->
</p>

---

BrewPHP brings Django's ideas to modern PHP: apps, URLconfs, views,
templates, an ORM, migrations, an automatic admin and a `manage.php` for
everything. The core is meant to be small enough to read in an afternoon.

## Get started in 30 seconds

```bash
composer create-project brewphp/skeleton myapp
cd myapp
php manage.php serve
```

Then open <http://127.0.0.1:8000/>.

## What the code looks like

```php
<?php
// config/urls.php: the root URLconf

declare(strict_types=1);

use BrewPHP\Http\Request;

return [
    path('', fn (Request $request) => 'Hello, world!', name: 'home'),
    path('blog/', include_urls('apps/blog/urls.php', namespace: 'blog')),
];
```

```php
<?php
// apps/blog/views.php

declare(strict_types=1);

namespace Apps\Blog;

use BrewPHP\Http\Request;
use BrewPHP\Http\Response;

function detail(Request $request, int $id): Response
{
    return render('blog/detail.php', ['id' => $id]);
}
```

```php
<?php
// apps/blog/urls.php

declare(strict_types=1);

use function Apps\Blog\detail;

return [
    path('posts/<int:id>/', detail(...), name: 'detail'),
];
```

`reverse('blog:detail', ['id' => 5])` gives `/blog/posts/5/`.

## Repositories

| Repository | What it is |
|---|---|
| [brewphp/brewphp](https://github.com/brewphp/brewphp) | The framework core (Composer package `brewphp/brewphp`) |
| [brewphp/skeleton](https://github.com/brewphp/skeleton) | The starter project used by `composer create-project` |
| [brewphp/docs](https://github.com/brewphp/docs) | The documentation, published at [docs.brewphp.dev](https://docs.brewphp.dev) |

A global installer is planned as the separate package `brewphp/installer`,
providing `brewphp new myapp`. The skeleton remains the main way to start.

## Roadmap

| Version | Scope |
|---|---|
| v0.1 | Router, views, request/response, settings, CLI |
| v0.2 | ORM (SQLite, MySQL, PostgreSQL) |
| v0.3 | Templates |
| v0.4 | Migrations and `startapp` |
| v0.5 | Auth, sessions, CSRF, forms |
| v0.6 | Automatic admin |

## Contributing

Contributions are welcome. Read the [contributing guide](https://github.com/brewphp/.github/blob/main/CONTRIBUTING.md)
and the [code of conduct](https://github.com/brewphp/.github/blob/main/CODE_OF_CONDUCT.md).
Report security issues privately as described in the
[security policy](https://github.com/brewphp/.github/blob/main/SECURITY.md).
