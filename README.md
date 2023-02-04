# Postgresql + PgAdmin на базе docker-compose

## Требования:

- docker
- docker-compose

## Команды:

- создать директорию 'pgadmin' и задать владельца: `$ mkdir pgadmin && sudo chown -R 5050:80 pgadmin`
- поднять контейнер: `$ docker-compose --compatibility up -d`
- остановить запущенный контейнер: `$ docker-compose --compatibility stop`
- запустить остановленный контейнер: `$ docker-compose --compatibility start`
- остановить и удалить контейнер и сеть: `$ docker-compose --compatibility down`
- удалить директории 'pgadmin', 'pgdata': `$ sudo rm -r pgadmin pgdata`

## Доступ к Postgres:

- **URL:** `localhost:5432`
- **Username:** `postgres`
- **Password:** `changeme`

## Доступ к PgAdmin:

- **URL:** `http://localhost:5050`
- **E-mail:** `pgadmin@example.com`
- **Password:** `admin`

## Коннект к Postgres из PgAdmin
- **Host name/address:** `postgres_container`
- **Port:** `5432`
- **Maintenance DB:** `postgres`
- **Password:** `changeme`

## Переменные окружения:

- `POSTGRES_DB`: по умолчанию — **postgres**
- `POSTGRES_USER`: по умолчанию — **postgres**
- `POSTGRES_PASSWORD`: по умолчанию — **changeme**
- `PGADMIN_DEFAULT_EMAIL`: по умолчанию — **pgadmin@example.com**
- `PGADMIN_DEFAULT_PASSWORD`: по умолчанию — **admin**
- `PGADMIN_CONFIG_SERVER_MODE`: **False**

## Первичная инициализация структуры БД:

- При выполнении команды `docker-compose up` будут выполнены все скрипты из директории `initdb`.
- Любые `*.sql` или `*.sh` файлы в этом каталоге будут рассматриваться как скрипты для инициализации БД.
- Если БД уже была проинициализирована ранее, то никакие изменения к ней применяться не будут.
- Если в каталоге присутствует несколько файлов, то они будут отсортированы по имени с использованием текущей локали (по умолчанию en_US.utf8).
- Если инициализация не нужна, достаточно очистить каталок `initdb` перед выполнением команды `docker-compose up`.

## Размещение данных БД:

- При выполнении команды `docker-compose up` рядом со скриптом создайтся директория `pgdata`, где будут располагаться файлы БД.
- При новой инициализации БД директорию `pgdata` можно удалить: `$ sudo rm -r pgdata`

## Размещение данных PgAdmin:

- Перед первым выполнении команды `docker-compose up` необходимо создать директорию `pgadmin` для данных PgAdmin и задать владельца:  
`$ mkdir pgadmin && sudo chown -R 5050:80 pgadmin`
- При новой инициализации БД директорию `pgadmin` можно очистить:  
`$ sudo rm -rf pgadmin/*`

## Параметры контейнера:

- В блоке кода `command:` заданы парметры БД, влияющие на производительность.
- Для использования параметров БД по умолчанию достаточно удалить блок кода `command:`.

<!-- -->

- В блоке кода `healthcheck:` задана периодическая проверка состояния/работоспособности БД и перезапуск контейнера при неполадках.
- Для отмены такой проверки достаточно удалить блок кода `healthcheck:`.

<!-- -->

- В блоке кода `deploy:` заданы ограничения ресурсов для контейнера с БД.
- Для отмены ограничений достаточно удалить блок кода `deploy:`.
