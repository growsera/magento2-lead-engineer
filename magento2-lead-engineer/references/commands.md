# Environment-aware command patterns

## Detect version and mode
- `bin/magento --version`
- `bin/magento deploy:mode:show`

## markshust/docker-magento (common patterns)
- Run CLI: `bin/magento <command>`
- Shell: `bin/bash` then run `bin/magento <command>`
- Container logs: `docker-compose logs php-fpm` (or `docker compose logs php-fpm`)

Confirm container names and compose tooling if unsure.

## Non-Docker host
- Run CLI: `php bin/magento <command>`
- Composer: `composer install` / `composer dump-autoload`

## Common Magento commands
- `bin/magento setup:upgrade`
- `bin/magento cache:status`
- `bin/magento cache:flush`
- `bin/magento indexer:reindex`
- `bin/magento setup:di:compile` (required in production mode)
- `bin/magento setup:static-content:deploy` (required in production mode)

Always state whether commands run inside the container or on the host.
