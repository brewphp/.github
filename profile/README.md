<div align="center">

# ☕ BrewPHP

**A small, Django-inspired PHP framework.**<br>
Easy to learn, a core you can read in an afternoon, zero runtime dependencies.

[![License: MIT](https://img.shields.io/badge/license-MIT-6F4E37?style=flat-square)](https://github.com/brewphp/brewphp/blob/main/LICENSE)
[![PHP 8.2+](https://img.shields.io/badge/php-8.2%2B-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![Docs](https://img.shields.io/badge/docs-docs.brewphp.dev-C8A27A?style=flat-square)](https://docs.brewphp.dev)

[Documentation](https://docs.brewphp.dev) ·
[Quick start](#-quick-start) ·
[Roadmap](#-roadmap) ·
[Contributing](https://github.com/brewphp/.github/blob/main/CONTRIBUTING.md)

</div>

---

BrewPHP brings Django's ideas to modern PHP: **apps**, **URLconfs**,
**views**, an **ORM**, **templates**, **migrations**, **auth and forms**, an
**automatic admin** and a `manage.php` for everything.

## 🚀 Quick start

```bash
composer create-project brewphp/skeleton myapp
cd myapp
php manage.php serve
```

Then open http://127.0.0.1:8000/.

## 👀 A taste

```php
// apps/blog/models.php
final class Post extends Model
{
    public static function fields(): array
    {
        return [
            'title' => new CharField(maxLength: 200),
            'body' => new TextField(),
            'published' => new BooleanField(default: false),
        ];
    }
}

// apps/blog/views.php
function index(Request $request): Response
{
    $posts = Post::objects()->filter(published: true)->orderBy('-id');

    return render('blog/index.html', ['posts' => $posts]);
}

// apps/blog/urls.php
return [
    path('', index(...), name: 'index'),
];
```

## 📦 Repositories

| Repository | Description |
|---|---|
| [**brewphp**](https://github.com/brewphp/brewphp) | The framework core, Composer package `brewphp/brewphp` |
| [**skeleton**](https://github.com/brewphp/skeleton) | Starter project for `composer create-project brewphp/skeleton` |
| [**docs**](https://github.com/brewphp/docs) | Documentation, published at [docs.brewphp.dev](https://docs.brewphp.dev) |
| [**.github**](https://github.com/brewphp/.github) | This profile and the shared community files |

## 🗺 Roadmap

| Version | Scope | Status |
|---|---|---|
| 0.1 | Router, views, request/response, settings, CLI | ✅ Done |
| 0.2 | ORM (SQLite, MySQL, PostgreSQL) | ✅ Done |
| 0.3 | Templates | ✅ Done |
| 0.4 | Migrations and `startapp` | ✅ Done |
| 0.5 | Auth, sessions, CSRF, forms | ✅ Done |
| 0.6 | Automatic admin | ✅ Done |

## 🤝 Contributing

Contributions are welcome. Start with the
[contributing guide](https://github.com/brewphp/.github/blob/main/CONTRIBUTING.md)
and the [code of conduct](https://github.com/brewphp/.github/blob/main/CODE_OF_CONDUCT.md).
Please report security issues privately, as described in the
[security policy](https://github.com/brewphp/.github/blob/main/SECURITY.md).
