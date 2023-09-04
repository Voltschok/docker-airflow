### Описание
В проекте по работе с Docker compose был собран образ для запуска в трех отдельных контейнерах Airflow, Postgres, Adminer. Написан DAG по загрузке сырых данных из файла в формате csv, аггрегации с помощью pandas и дальнейшей загрузки в БД с помощью sqlite3. 
Изменен конфиг файл для подключения SMTP  для отправки писем (через EmailOperator). Включена поддержка аутентификации: 
- дополнен пакет для работы входа по логину и паролю в Dockerfile,  
- Написан bash-скрипт для создания первого пользователя (user=admin, pass=admin) и вставлен в запуск в Dockerfile в качестве ENTRYPOINT.

### Структура репозитория
Внутри `project` расположены
1. Две папки:
- папка scripts, содержащая 
     - init.sh -  bash-скрипт для создания первого пользователя
- config/
     - airflow.cfg - измененный конфиг файл для подключения SMTP  для отправки писем 
 2. Файлы:
   - Dockerfile - с описание сборки образа
   - docker-compose.yml -  сценарий для разворачивания нескольких контейнеров из образа

 
