## Учебный проект infra_sp2 на базе YaMDb.

### Описание проекта ###

По адресу http://localhost. подключена документация API YaMDb. В ней описаны возможные запросы к API и структура ожидаемых ответов. Для каждого запроса указаны уровни прав доступа: пользовательские роли, которым разрешён запрос.

### Техническое описание проекта YaMDb. ###

Проект **YaMDb** собирает отзывы (*Review*) пользователей на произведения (*Titles*).

Произведения делятся на категории: (*Category*).

Произведению может быть присвоен жанр (*Genre*).

Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (*Review*) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — *рейтинг* (целое число). На одно произведение пользователь может оставить только один отзыв.

Отзыв может быть прокомментирован (*Сomment*) пользователями.

### Установка и запуск проекта:

* Клонировать репозиторий и перейти в него в командной строке:

```bash
git clone https://github.com/Kirill-Shutov/infra_sp2.git
cd infra_sp2
```

* Cоздать и активировать виртуальное окружение:
* Установить зависимости из файла requirements.txt:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

* Выполнить миграции:

```bash
cd api_yamdb
python3 manage.py migrate
```

* Создать суперпользователя (для раздачи прав админам):

```bash
python manage.py createsuperuser
```

* Запустить проект:

```bash
python manage.py runserver
```
### Шаблон наполнения env-файла:

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

### Запуска приложения в контейнерах:

1. Переходим в папку infra:

```cd
infra/
```

2. Собираем контейнер:

```
docker-compose up -d --build
```

3. Выполняем миграции:

```
docker-compose exec web python manage.py migrate
```

4. Создаем суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

5. Собираем статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

6. Для заполнения базы выполните команду:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

* Команда останавки контейнера:

```
docker-compose down -v
```

### Автор:
Студент Яндекс Практикума - Шутов Кирилл
