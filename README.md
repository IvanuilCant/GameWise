# Описание
GameWise — это инновационная образовательная платформа, предлагающая курсы в игровой форме, которые делают процесс обучения увлекательным и интерактивным. Платформа ориентирована на пользователей, желающих развить свои навыки в различных областях, таких как геймдизайн, программирование и творческое мышление.
## Наименование
GameWise - Обучение, которое увлекает!
## Предметная область
GameWise охватывает широкий спектр тем, связанных с обучением в различных сферах жизни. Используя игровые механики для обучения, платформа делает процесс более увлекательным и эффективным, позволяя пользователям развивать как профессиональные, так и личные навыки. GameWise стремится удовлетворить потребности самых разных пользователей — от студентов до профессионалов — предлагая им возможность учиться в удобном формате.
# Инструкция по использованию
## Зависимости
Для работы приложения требуется установить docker. Скрипты запуска работают на linux/macos. Для работы на windows требуется использовать эмуляцию работы unix, например git bash или cygwin.
## Необходимая подготовка
После установки докера требуется создать аккаунт на hub.docker.com и сгенерировать на нём personal access token.
Никнейм и токен нужно вставить в .env файл на соответсвующие места в двойых ковычках
```
DOCKERHUB_USERNAME="sample_username"
DOCKERHUB_TOKEN="sample_token"
```
## Запуск приложения
В папке находятся 3 скрипта для запуска, останоки и сборки приложения

 - build_and_push.sh собирает проект и загружает на докерхаб в соответтвии с .env
 - start.sh запускает проект в соответтвии с .env, требуется предварительная сборка
 - stop.sh останавливает проект в соответтвии с .env

Скрипты start и stop поддерживают частичную работу с проектам по средсвам передачи флагов:
-w/-f - Запустить web/frontend составляющую
-a/-b - Запустить api/backend составляющую
Если ни одного флага передано не было, то работа выполняется со всем проктом

# Данные
## Пользователи
| Название | Содержимое | Тип данных | Ограничения | Стандартное значение | 
| :------: | :--------: | :--------: | :---------: | :------------------: |
| username | имя пользователя | Char | длина не более 255, уникален| &#8212; | 
| email | почтовый адрес пользователя | String | уникален | &#8212; |
| is_active | может ли пользователь входить на сайт | Bool | &#8212; | True | 
| is_staff | является ли пользователь сотрудником | Bool | &#8212; | False |
| is_superuser | является ли пользователь суперюзером | Bool |&#8212; | False | 
| date_joined | дата последнего захода на сайт | DateTime | &#8212; | Now |
| profile_photo | аватар профиля | Image | &#8212; | &#8212; |


## Курсы
| Название | Содержимое | Тип данных | Ограничения | Стандартное значение | 
| :------: | :--------: | :--------: | :---------: | :------------------: |
| title | Название курса | Char | длина не более 255, уникален| &#8212; | 
| author | ID автора курса | ForeignKey | &#8212; | &#8212; |
| description | Опиасние курса | Text | длина не более 500 | null | 
| tags | Тэги курса | Char | длина не более 255 | &#8212; |
| content | Содержимое курса | Text | &#8212; | null | 

## Записи на курсы
| Название | Содержимое | Тип данных | Ограничения | Стандартное значение | 
| :------: | :--------: | :--------: | :---------: | :------------------: |
| course | ID курса | ForeignKey | &#8212; | &#8212; | 
| user | ID пользователя | ForeignKey | &#8212; | &#8212; |
| enrollment_date | Дата записи | DateTime | &#8212; | Now |

## Общие ограничения целостности
# Пользовательские роли
| Название роли | ответственность | количество пользователей |
| :-----------: | :-------------: | :----------------------: |
| User | Отсутствует | Не ограничено |
| Admin | Редактирование пользователей, создание и редактирование курсов | 5 |
# API 

| URL запроса | результат |
| :---------: | :-------: |
| /api/register/ | запрос данных у пользователя для регистрации на сайте |
| /api/login/ | запрос данных для авторизации на сайте |
| /api/profile/?userid={userid} | запрос к БД на получение данных о пользователе по его id |
| /api/courses/ | Выводит список всех доступных курсов |
| /api/courses/{course_id}/ | Возвращает API-ответ с детальной информацией о курсе с указанным id |
| /api/courses/{course_id}/enroll/ | Осуществляет регистрацию (запись) пользователя на курс с указанным id |
| /api/courses/create/ | Интерфейс для создания нового курса |
| /api/user/{userid}/courses | возвращает количество курсов по всем пользователям |
| /api/user/{int:user_id}/courses/ | посмотреть курсы конкретного пользователя | 
| /api/courses/users | посмотреть количество курсов всех пользователей |
| /api/users/{int:user_id}/edit/ | отредактировать информацию о пользователе |
| /api/delete_user/{int:user_id}/ | удалить из базы пользователя по id |

# Технологии разработки
## Язык программирования
Python 3.8
Node.js 20
## СУБД
sqlite3
# Тестирование
