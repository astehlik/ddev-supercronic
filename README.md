# ddev-supercronic

A [DDEV](https://ddev.com) add-on that installs
[supercronic](https://github.com/aptible/supercronic) as a cron runner in the
web container.

Unlike the system `cron` daemon, supercronic inherits the full container
environment, so all environment variables set by DDEV (e.g. `IS_DDEV_PROJECT`,
database credentials, `TYPO3_CONTEXT`) are automatically available to cron jobs
without any inline exports.

## Installation

```bash
ddev add-on get astehlik/ddev-supercronic
ddev restart
```

## Usage

Add one or more `*.cron` files to `.ddev/web-build/`. Each file uses standard
crontab syntax.

An example is provided at `.ddev/web-build/time.cron.example`. Rename it to
activate it:

```bash
mv .ddev/web-build/time.cron.example .ddev/web-build/time.cron
ddev restart
```

Example `.ddev/web-build/myproject.cron`:

```cron
* * * * * cd /var/www/html && vendor/bin/typo3 scheduler:run
```

## Removal

```bash
ddev add-on remove astehlik/ddev-supercronic
```

## Versioning

The add-on version tracks the supercronic version it ships. A GitHub Actions
workflow checks for new supercronic releases every Monday and automatically
publishes a new release.
