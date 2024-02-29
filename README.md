# Контейнеризация (семинары)
Задание 1:

1) Для создания сервиса, состоящего из 2 различных контейнеров (веб и база данных), я использую Docker Compose. Создам файл docker-compose.yml со следующим содержимым:


version: '3'
services:
  web:
    build: ./web
    ports:
      - 80:80
  db:
    build: ./db


В данном файле описаны два сервиса: web и db. Контейнер web будет собран из директории ./web (где располагается Dockerfile для веб-приложения) и будет проброшен порт 80. Контейнер db будет собран из директории ./db (где располагается Dockerfile для базы данных).

2) Далее необходимо создать 3 сервиса в каждом окружении (dev, prod, lab). Для этого воспользуюсь возможностью описания нескольких секций services в файле docker-compose.yml для каждого окружения:


version: '3'
services:
  web:
    environment:
      - ENV=dev
  db:
    environment:
      - ENV=dev

dev:
  services:
    web:
      environment:
        - ENV=dev
    db:
      environment:
        - ENV=dev

prod:
  services:
    web:
      environment:
        - ENV=prod
    db:
      environment:
        - ENV=prod

lab:
  services:
    web:
      environment:
        - ENV=lab
    db:
      environment:
        - ENV=lab


Здесь добавлены секции dev, prod и lab, каждая из которых содержит описание сервисов web и db с соответствующими переменными окружения ENV.

3) Для того, чтобы на каждой ноде было по 2 работающих контейнера, необходимо использовать Docker Swarm. После настройки Swarm можно будет разворачивать сервисы на разных нодах. Количество контейнеров будет автоматически масштабироваться в зависимости от доступных ресурсов на нодах.

4) Для зафиксирования выводов необходимо сохранить конфигурационный файл docker-compose.yml, логи работы контейнеров, историю команд и сделать скриншоты, демонстрирующие работу приложения в разных окружениях.

Задание 2*:

1) Для создания двух Docker-файлов, описывающих сервисы, создам файлы web.dockerfile и db.dockerfile с необходимым содержимым.

web.dockerfile:


FROM nginx:latest
COPY ./html /usr/share/nginx/html


db.dockerfile:


FROM mysql:latest
ADD ./database.sql /docker-entrypoint-initdb.d


2) Повторю задание 1 для двух окружений lab и dev, используя созданные Docker-файлы и файлы конфигурации docker-compose.dev.yml и docker-compose.lab.yml.

docker-compose.dev.yml:


version: '3'
services:
  web:
    build:
      context: .
      dockerfile: web.dockerfile
    environment:
      - ENV=dev
  db:
    build:
      context: .
      dockerfile: db.dockerfile
    environment:
      - ENV=dev


docker-compose.lab.yml:


version: '3'
services:
  web:
    build:
      context: .
      dockerfile: web.dockerfile
    environment:
      - ENV=lab
  db:
    build:
      context: .
      dockerfile: db.dockerfile
    environment:
      - ENV=lab


3) Для проверки и зафиксирования результатов выполнения задания необходимо сохранить файлы docker-compose.dev.yml, docker-compose.lab.yml, логи работы контейнеров, историю выполнения команд и скриншоты, демонстрирующие работу приложения в окружениях lab и dev.
![2_5](homework/2_5.JPG)
![2_6](homework/2_6.JPG)
![2_7](homework/2_7.JPG)
![2_9](homework/2_9.JPG)
*Подготовил студент GeekBrains* **`Агаджанян Мигель`**, 
Seminar_5_containerization
