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
      - ENV=lab<img width="1440" alt="Снимок экрана 2024-02-29 в 15 53 02" src="https://github.com/minobol/g/assets/120034142/f19f81f4-ddaf-4b57-b96f-e515a6512d2f">
<img width="1440" alt="Снимок экрана 2024-02-29 в 16 04 25" src="https://github.com/minobol/g/assets/120034142/46889f94-6ce1-4237-86c8-5bed175a3e5b"><img width="1440" alt="Снимок экрана 2024-02-29 в 16 04 40" src="https://github.com/minobol/g/assets/120034142/63f492dd-b222-4f9b-afb3-81ea8fb3e7d9">
<img width="1440" alt="Снимок экрана 2024-02-29 в 16 05 13" src="https://github.com/minobol/g/assets/120034142/2cb7f490-e0ee-4a70-82ea-e9d32d49e13f">
<img width="1440" alt="Снимок экрана 2024-02-29 в 16 44 20" src="https://github.com/minobol/g/assets/120034142/64388fa8-e635-4f59-89c3-cb0a436c0e4b">


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
