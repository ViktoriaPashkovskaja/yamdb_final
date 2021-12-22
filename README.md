##Описание сервиса 
Автор: Пашковская Виктория 
####Проект YaMDb 
Cобирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

###Установка сервиса 
Скопируйте проект к себе на компютер git clone https://github.com/Lookin44/infra_sp2.git 
Создайте файл .env со значениями: DB_ENGINE=django.db.backends.postgresql DB_NAME=postgres POSTGRES_USER=postgres POSTGRES_PASSWORD=postgres DB_HOST=db DB_PORT=5432 EMAIL_HOST_PASSWORD=<Ваш пароль от почты> Запустите Docker: sudo docker-compose up Выполните миграции внутри докера sudo docker-compose exec web python manage.py migrate --noinput Создайте суперюзера внутри докера sudo docker-compose exec web python manage.py createsuperuser Соберите всю статику внутри докера sudo docker-compose exec web python manage.py collectstatic --no-input Загрузите тестовые данные sudo docker-compose exec web python manage.py loaddata fixtures.json

###Алгоритм регистрации пользователей 
Пользователь отправляет запрос с параметром email и username на /auth/email/. YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email . Пользователь отправляет запрос с параметрами email, username и confirmation_code на /auth/token/, в ответе на запрос ему приходит token (JWT-токен). При желании пользователь отправляет PATCH-запрос на /users/me/ и заполняет поля в своём профайле (описание полей — в документации).

###Пользовательские роли 
Аноним — может просматривать описания произведений, читать отзывы и комментарии. 
Аутентифицированный пользователь — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии. 
Модератор — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии. 
Администратор — полные права на управление проектом и всем его содержимым. Может создавать и удалять категории и произведения. Может назначать роли пользователям. 
Администратор Django — те же права, что и у роли Администратор.

###Информация по запросам 
Запустите сервер. Перейдите на http://localhost:8000/redoc/

![yamdb_final](https://github.com/ViktoriaPashkovskaja/yamdb_final/workflows/yamdb_final/badge.svg)
###На боевом сервере http://51.250.27.153/
