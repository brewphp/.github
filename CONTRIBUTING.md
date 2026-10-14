# Contributing to BrewPHP

Thank you for helping. This guide covers all BrewPHP repositories:
[brewphp](https://github.com/brewphp/brewphp) (the framework),
[skeleton](https://github.com/brewphp/skeleton) (the starter project) and
[docs](https://github.com/brewphp/docs) (the documentation).

By taking part you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).
Never report security problems in public issues: follow the
[security policy](SECURITY.md) instead.

## Setting up

The repositories are meant to sit side by side in one folder. The skeleton
uses a Composer path repository pointing to `../brewphp`, so it always runs
against your local framework checkout.

```bash
mkdir brewphp-workspace && cd brewphp-workspace
git clone git@github.com:brewphp/brewphp.git
git clone git@github.com:brewphp/skeleton.git
git clone git@github.com:brewphp/docs.git

cd brewphp
composer install
```

To try your changes in a real project:

```bash
cd ../skeleton
composer install
cp .env.example .env
php manage.php key:generate
php manage.php serve
```

You need PHP 8.2 or newer and Composer 2.

## Rules

- **PHP 8.2+**, `declare(strict_types=1);` in every file, full type hints.
- **PSR-4** autoloading and **PSR-12** code style.
- **Zero runtime dependencies** in the framework core. Development tools
  (PHPUnit, PHPStan, PHP-CS-Fixer) are fine. Ask in an issue before
  proposing a new dependency of any kind.
- **Small and readable.** Prefer clear code over clever code; no magic that
  cannot be explained in one documentation paragraph.
- **Every feature ships complete:** code in `brewphp/`, PHPUnit tests, a
  page (or section) in `docs/`, and an entry in `CHANGELOG.md`.
- **One repository per commit.** Commit separately in each repository and
  never mix repositories in one commit.
- Documentation and code comments are written in English.

## Commit messages

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(routing): add a uuid path converter
fix(http): keep the query string when appending a slash
docs(views): explain class-based view dispatch
test(console): cover key:generate without a .env file
refactor(core): split ErrorHandler page rendering
chore: update PHPStan to 2.1
```

Use the area as the scope (`core`, `http`, `routing`, `views`, `middleware`,
`console`, `orm`, `templates`...). Mark breaking changes with `!`, for
example `feat(routing)!: rename group() to route_group()`.

## Checks

Run these in `brewphp/` before opening a pull request:

```bash
composer test     # PHPUnit
composer stan     # PHPStan, level 8
composer cs       # PHP-CS-Fixer in dry-run mode (composer cs:fix applies fixes)
composer ci       # all three
```

All three must pass. Tests should cover both the expected behaviour and the
error cases.

## Building the documentation

The docs use MkDocs with the Material theme.

```bash
cd docs
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve                     # live preview at http://127.0.0.1:8000
mkdocs build --strict            # what CI runs
```

Every code block in the docs must be copy-paste runnable, and every page
must stay in sync with the code. If you change behaviour, update the page
in the same pull request series.

## Pull requests

1. Open an issue first for anything bigger than a small fix, so we can agree
   on the approach.
2. Create a branch from `main` (for example `feat/uuid-converter`).
3. Keep each pull request to one repository. A feature that needs code and
   docs gets one pull request in `brewphp` and one in `docs`; link them.
4. Fill in the pull request template checklist.
5. A maintainer reviews it. Expect questions and small change requests;
   that is a normal part of the process.
6. Once approved and green, a maintainer merges it.

## Reporting bugs and asking for features

Use the issue forms in each repository. For bugs, include the BrewPHP and
PHP versions and the smallest steps that reproduce the problem.
