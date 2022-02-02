![Yamdb_workflow](https://github.com/DenisKirichenko24/foodgram-project-react/actions/workflows/foodgram_workflow.yml/badge.svg)

# Яндекс.Практикум. Python backend. Diplom Foodgram

## Содержание
- [Описание_проекта](#Описание_проекта)
- [Технологии](#Технологии)
- [Запуск проекта](#Запуск_проекта)
- [Тесты](#Тесты)
- [Автор](#Автор)

### <a name="Описание_проекта">Описание</a>

Foodgram реализован для публикации рецептов. Авторизованные пользователи могут 
подписываться на понравившихся авторов, добавлять рецепты в избранное, 
в покупки, скачать список покупок ингредиентов для добавленных в покупки 
рецептов.


### <a name="Технологии">Технологии</a>

В проекте применены
- **Django REST Framework**, 
- **Python 3**,
- **PostgreSQL**,
- **Docker**, 
- **Nginx**,
- **Gunicorn**,
- **Git**, 
- Аутентификация реализована с помощью **токена**.

### <a name="Запуск проекта">Запуск проекта</a>

- Установите Docker на ваш сервер:
```python
 sudo apt install docker.io
```

- Установите Docker-compose на сервер:
```python
 sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose
```

- Скопируйте на сервер файлы Docker-compose.yml и nginx.conf из папки infra/. Укажите в конфиге ваш IP.
```python
scp docker-compose.yml admin@51.250.18.186:/home/admin/docker-compose.yml
scp nginx.conf admin@51.250.18.186:/home/admin/nginx.conf
```

- При первом деплоее локально в файле foodgram_workflow.yml в deploy указываем флаг --build:
```python
 sudo docker-compose rm -f backend --build
```

- После успешного деплоя зайдите на боевой сервер и выполните команды (только после первого деплоя):
    Собрать статические файлы в STATIC_ROOT:
```python
  docker-compose exec backend python3 manage.py collectstatic --noinput
```

- После запуска контейнеров выполните команды в терминале:
```python
 docker-compose exec backend python manage.py makemigrations
 docker-compose exec backend python manage.py migrate --noinput
```

- Создаём суперпользователя
```python
 docker-compose exec backend python manage.py createsuperuser
```

- Загружаем ингредиенты в базу данных (необязательно):
```python
 docker-compose exec backend python manage.py loaddata ingredients.json
```

- Запуск контейнеров выполняется командой:
```python
 docker-compose up
```

- Остановка контейнеров выполняется командой:
```python
 docker-compose stop
```

### <a name="Тесты">Тесты</a>
```python
  flake8, isort
```

### <a name="Автор">Авторы</a>
```
 Денис Кириченко 
```
