# Описание

Async API сервис для получения контента: жанры, персоны, фильмы.

# Авторы
* [@likeinlife](https://github.com/likeinlife)
* [@maxim-zaitsev](https://github.com/maxim-zaitsev)

# Вклад @likeinlife

- ETL (submodule)
- API
- Сервис, тесты: жанры, персоны

# Вклад @maxim-zaitsev

- Redis caching
- Сервис, тесты: поиск по фильмам
- Модели
- Nginx

# Установка
- Скопировать файл ./.env.example в файл ./.env
- Заполнить .env своими данными
- через Makefile выполнить команды:
  - make up
  - make fill (потребуется несколько минут для загрузки дамп в ElasticSearch)

# Запуск/остановка
- make up - запуск
- make fill - заполнить данными elasticsearch
- make down - удалить созданные контейнеры
- make downv - удалить созданные контейнеры, включая volumes

# Тестирование
- make test

# Адрес api
http://localhost:80

## Адрес для проверки удачного запуска
http://localhost:80/api/openapi

# Переменные окружения
Смотреть .env.example

# task_00: Проведите 2 ревью
https://github.com/likeinlife/Async_API_sprint_2/pull/14
https://github.com/likeinlife/Async_API_sprint_2/pull/13

https://github.com/likeinlife/Async_API_sprint_1/pull/17
https://github.com/likeinlife/Async_API_sprint_1/pull/16

# Дампы elastic
ETL-процесс сделан в другом репозитории, т.к. это независимые сервисы.
https://github.com/likeinlife/YA-ETL
Дампы сделаны с помощью инструмента elasticsearch-dump:
https://github.com/elasticsearch-dump/elasticsearch-dump

# Структура индексов
<details>
<summary>movie</summary>

```
{
    id: uuid,
    imdb_rating: float,
    genre: {
        id: uuid,
        name: str
    },
    title: string,
    description: string,
    directors: [
        {
            id: uuid,
            name: string
        }
    ],
    actors: [
        {
            id: uuid,
            name: string
        }
    ],
    writers: [
        {
            id: uuid,
            name: string
        }
    ]
}
```
</details>

<details>
<summary>genre</summary>

```
{
    id: uuid,
    name: string,
    description: string,
    movies: [
        {
            id: uuid,
            title: string,
            imdb_rating: float
        }
    ]
}
```
</details>

<details>
<summary>person</summary>

```
{
    id: uuid,
    name: string,
    movies: [
        {
            id: uuid,
            title: string,
            imdb_rating: float,
            roles: [string]
        }
    ]
}
```
</details>
