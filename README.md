# API для социальной сети Yatube

REST API для учебной социальной сети Yatube. Позволяет управлять публикациями, комментариями, подписками и просматривать тематические группы.

## 🛠 Стек технологий
- Python 3.12
- Django 5.1
- Django REST Framework 3.15
- Djoser + SimpleJWT для аутентификации
- SQLite (для разработки)

## 🚀 Установка и запуск

1. Клонируйте репозиторий:
```bash
git clone https://github.com/ваш-username/api-final-yatube-main.git
cd api-final-yatube-main

2. Создайте и активируйте виртуальное окружение:
python -m venv venv
Для Windows:
venv\Scripts\activate
Для Linux/macOS:
source venv/bin/activate

3. Установите зависимости:
pip install -r requirements.txt

4. Примените миграции:
python manage.py migrate
5. Запустите сервер:
python manage.py runserver

Документация API доступна по адресу:
http://127.0.0.1:8000/redoc/

Примеры запросов
Получение токена (аутентификация)
POST /api/v1/jwt/create/
Content-Type: application/json

{
  "username": "testuser",
  "password": "1234567"
}

Ответ (200 OK):
{
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}


Создание публикации
POST /api/v1/posts/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "text": "Мой первый пост!",
  "group": 1
}

Ответ (201 Created):
{
  "id": 1,
  "text": "Мой первый пост!",
  "author": "testuser",
  "pub_date": "2024-01-01T12:00:00Z",
  "image": null,
  "group": 1
}


Подписка на пользователя
POST /api/v1/follow/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "following": "username_to_follow"
}

Ответ (201 Created):
{
  "user": "testuser",
  "following": "username_to_follow"
}


Ошибка при подписке на себя
POST /api/v1/follow/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "following": "testuser"
}

Ответ (400 Bad Request):
{
  "following": ["Нельзя подписаться на самого себя"]
}


Автор
Артём Шастунов

Проект выполнен в рамках обучения на Яндекс.Практикуме
