# Debugging (developer mode, 500 errors)

## First checks
1. Reproduce and capture the report ID (if shown).
2. Check `var/report/<id>`.
3. Review `var/log/exception.log`, `var/log/system.log`, and `var/log/debug.log`.

## Code and DI checks
- Inspect `generated/`, `var/di`, and `var/cache` for stale artifacts.
- Confirm module status: `bin/magento module:status`.
- Run `bin/magento setup:upgrade` after module changes.

## Docker-specific checks
- Review container logs: `docker-compose logs php-fpm` (or `docker compose logs php-fpm`).
- Ensure file permissions and volume mounts are correct.

## Developer-mode tools
- Enable template hints only in developer mode when needed.
- Avoid enabling developer mode on production; use staging if possible.
