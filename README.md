# php-ianf-strict-template

A [copier](https://copier.readthedocs.io) template for a PHP project that starts on [php-ianf-strict-baseline](https://github.com/ianflanagan1/php-ianf-strict-baseline) and passes its own `devbox run -- task check` from the first commit. It is the PHP counterpart of [ts-ianf-strict-template](https://github.com/ianflanagan1/ts-ianf-strict-template) and [go-ianf-strict-template](https://github.com/ianflanagan1/go-ianf-strict-template).

```sh
copier copy --trust gh:ianflanagan1/php-ianf-strict-template my-project
```

`--trust` lets copier run the template's one task, `composer install` inside the new project's devbox, which writes the lockfile that `devbox run -- task setup` installs from.

## What a project gets

- devbox pinning PHP, Composer and go-task, and a `Taskfile.yml` with `setup`, `check`, `format` and `lint-file` tasks (`lint-file` is what the [static-checks](https://github.com/ianflanagan1/static-checks) hooks run on each edited file)
- php-ianf-strict-baseline's PHPStan, deptrac and Pint configs, with `php-ianf-strict-baseline verify` in `check`
- the Composer name `ianflanagan1/<name>` and the root namespace `IanFlanagan\<Name>\` on `src/`, from the project name
- an entrypoint in `bin/<name>`, empty `src/` and `tests/`, PHPUnit, a GitHub Actions workflow that runs `devbox run -- task check`
- a `.gitignore` with `/cache/`, where PHPStan, deptrac and PHPUnit keep their caches
- a `CLAUDE.md` to fill in
- `.config/ianf-repo-tools.toml` with the integration mode you choose (`direct`, `pr-rebase` or `pr-merge`), which [repo-list and repo-fix](https://github.com/ianflanagan1/repo-tools) read; there's no default

php-ianf-strict-baseline has no releases yet, so a project requires its `dev-main` from GitHub, and `composer.lock` pins the commit. Unlike ts-ianf-strict-baseline, it doesn't ship the `check` task's commands, so they live in the project's `Taskfile.yml`.

## Keeping a project current

```sh
copier update --trust
```

merges what changed in the template since the project was made (it reads `.copier-answers.yml`), leaving conflicts to resolve as with a git merge.

## Development

```sh
devbox run -- task check   # generate a project and run its check
```

`devbox run -- task check BASELINE=/path/to/php-ianf-strict-baseline` installs php-ianf-strict-baseline from a local checkout, to try changes that aren't pushed yet.
