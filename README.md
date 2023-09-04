### Описание
В проекте по работе с Docker compose был собран образ Airflow, Postgres. Витрины данных были спроектированы и рассчитаны с использованием PySpark. Расчет витрин был автоматизирован с помощью SparkSubmitOperator в DAG Airflow.

### Структура репозитория

Внутри `src` расположены две папки:
- `/src/dags`
	- de-sprint-7-project-dag-initial-load.py — Инициальная загрузка данных выполняется в ручную (однократно)
	- de-sprint-7-project-dag1.py — DAG обновляет слой STG из источника и производит расчет метрик витрины 1 и 3 (на заданную глубину ежедневно)
 	- de-sprint-7-project-dag2.py — производит расчет метрик витрины 2 (на заданную глубину еженедельно)
- `/src/scripts`

    - load_data.py — Job инициальной загрузки;
    - update_data.py — Job обновления STG;
    - 1st_vitrin.py — Job расчета метрик пользователя;
    - 2nd_vitrin.py — Job расчета метрик по зонам (городам);
    - 3d_vitrin.py — Job расчета метрик для витрины с рекомендациями друзей.

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
