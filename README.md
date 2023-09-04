# docker-airflow
- project/
   - Dockerfile
   - docker-compose.yml
   - scripts/
     - init.sh
   - config/
     - airflow.cfg

Написан DAG по загрузке сырых данных из файла в формате csv, аггрегации с помощью pandas и дальнейшей загрузки в БД с помощью sqlite3.
Изменен конфиг файл для подключения SMTP  для отправки писем (через EmailOperator)
 
Включена поддержка аутентификации:
- дополнен пакет для работы входа по логину и паролю в Dockerfile,  
- Написан bash-скрипт для создания первого пользователя (user=admin, pass=admin) и вставлен в запуск в Dockerfile в качестве ENTRYPOINT

Добавлен новый сервис (adminer) в docker-compose для доступа к базе данных Airflow
