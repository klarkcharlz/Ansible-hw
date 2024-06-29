# Ansible Playbook for Installing Clickhouse, Vector, and Lighthouse

## Описание

Этот Ansible playbook предназначен для установки и настройки Clickhouse, Vector и Lighthouse на серверах. Он выполняет следующие задачи:

1. Скачивает и устанавливает Clickhouse client и server.
2. Обеспечивает запуск службы Clickhouse.
3. Создаёт базу данных в Clickhouse.
4. Скачивает и устанавливает Vector.
5. Настраивает Vector с помощью шаблона Jinja2.
6. Обеспечивает запуск службы Vector под supervisord.
7. Устанавливает и настраивает Lighthouse.
8. Обеспечивает запуск службы Nginx для Lighthouse.

## Требования

- Ansible 2.9 или новее
- Серверы должны работать под управлением Debian-based ОС

## Структура Playbook

### Установка Clickhouse

- Скачивает Clickhouse client, server и common static пакеты.
- Устанавливает пакеты.
- Обеспечивает запуск службы Clickhouse.
- Создаёт базу данных с именем `logs`.

### Установка и настройка Vector

- Скачивает Vector.
- Распаковывает Vector в указанную директорию установки.
- Настраивает Vector с помощью шаблона Jinja2.
- Обеспечивает запуск службы Vector под supervisord.

### Установка и настройка Lighthouse

- Устанавливает необходимые пакеты, включая Nginx и unzip.
- Настраивает Nginx с использованием шаблона Jinja2.
- Скачивает и распаковывает Lighthouse в директорию `/var/www`.
- Перезапускает службу Nginx для применения новых настроек.


## Использование

### Для запуска этого playbook используйте следующие команды:

Проверка синтаксиса и ошибок линтинга:
```
ansible-lint site.yml
```

Запуск playbook в режиме проверки:
```
ansible-playbook site.yml -i prod.yml --check
```

Запуск playbook с режимом diff для просмотра изменений:
```
ansible-playbook site.yml -i prod.yml --diff
```

Повторный запуск playbook для проверки идемпотентности:
```
ansible-playbook site.yml -i prod.yml --diff
```

## Handlers

1. Start Clickhouse Service: Перезапускает службу Clickhouse в случае изменений в пакетах Clickhouse.
2. Restart Vector Service: Перезапускает службу Vector в случае изменений в конфигурации Vector.
3. Restart Nginx Service: Перезапускает службу Nginx в случае изменений в конфигурации Nginx.

## Переменные

- clickhouse_version: Версия Clickhouse для установки.
- vector_version: Версия Vector для установки.
- vector_install_dir: Директория для установки Vector.
- vector_config_dir: Директория для размещения конфигурационного файла Vector.
- vector_config_file: Путь к конфигурационному файлу Vector.
- vector_download_url: URL для скачивания tarball Vector.
- lighthouse_package: URL для скачивания пакета Lighthouse.
