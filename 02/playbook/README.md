# Ansible Playbook for Installing Clickhouse and Vector

## Описание

Этот Ansible playbook предназначен для установки и настройки Clickhouse и Vector на серверах. Он выполняет следующие задачи:

1. Скачивает и устанавливает Clickhouse client и server.
2. Обеспечивает запуск службы Clickhouse.
3. Создаёт базу данных в Clickhouse.
4. Скачивает и устанавливает Vector.
5. Настраивает Vector с помощью шаблона Jinja2.
6. Обеспечивает запуск службы Vector под supervisord.

## Требования

- Ansible 2.9 или новее
- Серверы должны работать под управлением Debian-based ОС


## Структура Playbook
### Playbook состоит из двух основных play:

- 1.Установка Clickhouse
  - 1.1. Скачивает Clickhouse client, server и common static пакеты. 
  - 1.2. Устанавливает пакеты, если они ещё не установлены.
  - 1.3. Обеспечивает запуск службы Clickhouse.
  - 1.4. Создаёт базу данных с именем logs.
- 2.Установка и настройка Vector
  - 2.1. Скачивает tarball Vector.
  - 2.2. Распаковывает tarball в указанную директорию установки.
  - 2.3. Настраивает Vector с помощью шаблона Jinja2.
  - 2.4. Обеспечивает запуск службы Vector под supervisord.


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


## Переменные

- clickhouse_version: Версия Clickhouse для установки.
- vector_version: Версия Vector для установки.
- vector_install_dir: Директория для установки Vector.
- vector_config_dir: Директория для размещения конфигурационного файла Vector.
- vector_config_file: Путь к конфигурационному файлу Vector.
- vector_download_url: URL для скачивания tarball Vector.
