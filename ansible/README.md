# Пример ansible-репозитория

## Список сервисов
Устанавливает следующие сервисы через systemd:
- ntpd
- atop
- node_exporter

## Обратите внимание

Ansible понимает два варианта inventory-файлов - INI и YAML. На мой взгляд формат INI хорош, когда структура групп и серверов не слишком сложна. Второй более объемный получается, зато его легче читать, когда иерархия групп сложная. По функционалу они совпадают. Я привел оба варианта с идентичным содержимым.

## Перед установкой

1. Убедиться, что inventory.ini файл настроен верно.
2. Отредактировать `group_vars/all/secret.yml` (vault-pass = `Zelda`):
```bash
ansible-vault edit group_vars/all/secret.yml
```

## Как пользоваться

Проверить все (dry-run):
```bash
ansible-playbook deploy-stage.yml --diff --check
```

Настроить все:
```bash
ansible-playbook deploy-stage.yml --diff
```

Настроить все, но только на группе stage:
```bash
ansible-playbook deploy-stage.yml --limit stage
```

Настроить только atop:
```bash
ansible-playbook deploy-stage.yml --tags atop
```

Настроить только ntpd:
```bash
ansible-playbook deploy-stage.yml --tags ntpd
```
