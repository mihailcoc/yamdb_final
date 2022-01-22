# yamdb_final
yamdb_final

#Проект: запуск docker-compose
### Проект развёртывается в Docker.
### В проекте оформлены docker-compose.yaml nginx/default.com .env Dockerfile
### В проекте использована технология Docker.




Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/mihailcoc/yamdb_final.git
```

```
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
. env/bin/activate 
source env/Scripts/activate 
```

```
python3 -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install django-adaptors
pip install environ
pip install psycopg2-binary
pip install wheel
pip install pillow
pip install -r requirements.txt
```
Выполнить миграции:

```
python3 manage.py makemigrations
python3 manage.py migrate auth
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```
Удалить все ранее установленые контейнеры по проекту infra_sp2.
```
cd infra
sudo docker-compose down -v
sudo docker system prune
```
Удаляем volumes и всех созданных юзеров.
```
sudo docker-compose down -v
sudo docker-compose down
sudo docker system prune
```
Затем выполнить миграции.
Миграции нужно делать внутри контейнера а не снаружи.
```
sudo docker-compose up -d --build
sudo docker-compose exec web python manage.py collectstatic --no-input

sudo docker-compose exec web python manage.py makemigrations
sudo docker-compose exec web python manage.py migrate auth
sudo docker-compose exec web python manage.py migrate --run-syncdb
```
Заново создаем контейнеры.
```
sudo docker-compose up -d --build
```
Создать контейнер.
```
sudo docker build -t yamdb . 
```
Посмотреть  image  контейнеров.
```
sudo docker image ls 
```
Удалить image
```
sudo docker image rm 3e57319a7a3a
```

Посмотреть ID контейнеров.
```
sudo docker ps -a
```
Остановить контейнер.
```
sudo docker container stop cdd583f87d9e
```
Удалить контейнер.
```
sudo docker container rm cdd583f87d9e
```

Запустить все неактивные контейнеры.
```
sudo docker-compose up
```
Пересобрать контейнеры и запустить их.
```
sudo docker-compose up -d --build
```
Собрать образ и запустить контейнер.
Команды должны выполняться из директории
в которой лежит Dockerfile.
```
sudo docker build .
```
Запустить контейнер из образа с image_id.
```
sudo docker image ls

sudo docker run -p 5000:5000 bd94675b6e4e 
```

Залогиниться на Dockerhub.
```
sudo docker login --username rozamundpike
```
Присвоить tag к image и отправить image на Dockerhub.
```
sudo docker tag bd9 rozamundpike/infra_sp2:infra_sp2
sudo docker push rozamundpike/infra_sp2:infra_sp2
```
![example event parameter]https://github.com/mihailcoc/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg