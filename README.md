# Learning Log

Веб-приложение на Django для ведения учебного дневника: пользователи регистрируются, создают темы и добавляют к ним записи.

## Возможности

- регистрация и вход пользователей
- создание тем и записей
- редактирование записей
- каждый пользователь видит только свои темы

## Технологии

Python, Django, SQLite, django-bootstrap4, Gunicorn, WhiteNoise, Docker Compose

## Запуск через Docker Compose

1. Создайте файл `.env` в корне проекта (пример ниже).
2. Выполните:

```
docker compose up --build -d
```

3. Откройте в браузере `http://<IP-сервера>:<APP_PORT>/`.

Остановить приложение:

```
docker compose down
```

## Переменные окружения (`.env`)

| Переменная | Назначение |
|---|---|
| `DJANGO_SECRET_KEY` | секретный ключ Django |
| `DJANGO_DEBUG` | режим отладки (`True` или `False`) |
| `DJANGO_ALLOWED_HOSTS` | разрешённые адреса через запятую |
| `DJANGO_CSRF_TRUSTED_ORIGINS` | доверенные адреса для форм, например `http://192.168.1.11:20010` |
| `DJANGO_USE_HTTPS` | включать ли защищённые cookie (`True` или `False`) |
| `SQLITE_PATH` | путь к базе внутри контейнера, `/app/data/db.sqlite3` |
| `APP_BIND_IP` | на каком адресе публиковать порт |
| `APP_PORT` | внешний порт приложения |

Пример `.env`:

```
DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=192.168.1.11,localhost,127.0.0.1
DJANGO_CSRF_TRUSTED_ORIGINS=http://192.168.1.11:20010
DJANGO_USE_HTTPS=False
SQLITE_PATH=/app/data/db.sqlite3
APP_BIND_IP=0.0.0.0
APP_PORT=20010
```

Файл `.env` не хранится в репозитории: создайте его на сервере.

## Локальный запуск без Docker

```
python -m venv ll_env
ll_env\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

На Linux/macOS активация: `source ll_env/bin/activate`.