# nokschedule - Расписание Новоскольского колледжа
<img width="1902" height="929" alt="изображение" src="https://github.com/user-attachments/assets/1f118476-6ec0-43fa-beb8-80ec69e43aa5" />
<img width="1900" height="933" alt="изображение" src="https://github.com/user-attachments/assets/2bf2b9c7-dca9-48d1-a604-b8cb35975f2e" />

## Описание проекта

Веб-приложение для управления расписанием занятий в колледже позволяет пользователям (администраторам, преподавателям и студентам) эффективно создавать, редактировать и просматривать расписание пар. Оно поддерживает гибкую настройку расписаний, их изменение по дням недели, отображение информации о корпусах, группах и преподавателях.

Приложение включает несколько основных функций, таких как логирование действий, контроль доступа, экспорт расписания в PDF и поддержка изменений в расписании на конкретные даты и т.д.

Исходный проект расписании был взят с Рязанского Колледжа Электроники. (Автор **[@GreenBabyBorn](https://github.com/GreenBabyBorn/sposchedule)**)

Большая благодарность за помощь ребятам [@AverageDragonTail](https://github.com/AverageDragonTail) и [@motionarium](https://github.com/motionarium)

## Лицензия

Приложение распространяется по лицензии [Apache License 2.0](LICENSE).

## Инструкции по установке
**1. Клонировать репозиторий**

    git clone https://github.com/ki4arl/nokschedule/

**2. Перейти в директорию проекта:**

    cd /nokschedule

**3. Настройка файла окружения .env для backend**


    cd /backend
    cp .env.example .env
    nano .env
 
>Изменить значения DB_USERNAME и DB_PASSWORD на личные данные.<br/>
Рекомендуется использовать локальный IP-адрес вместо 127.0.0.1. Например: 192.168.1.3<br/>
Изменить значение APP_URL на адрес вашего сайта, например: rasp.noskolagrokol.ru<br/>
Для параметра APP_KEY, придумайте уникальную последовательность из 32 символов. Пример: 0P5GD70N7y5ggkbOkCLBqIZeoJT5bc==<br/>
Укажите ваше доменное имя в параметре SESSION_DOMAIN, например: .noskolagrokol.ru<br/>
Включите свой сайт и поддомен API в SANCTUM_STATEFUL_DOMAINS, например: raspapi.noskolagrokol.ru, rasp.noskolagrokol.ru<br/>

**4. Настройка файла окружения .env для frontend**

    cd ..
    cd /frontend
    cp .env.example .env
    nano .env
>Добавьте в VITE_API_URL ссылку на ваш API (backend) сайта. Например: https://raspapi.noskolagrokol.ru.

**5. Настройка файла окружения .env для корневого файла**

    cd ..
    cp .env.example .env
    nano .env
>Изменить значения для параметров DB_USERNAME и DB_PASSWORD, чтобы они соответствовал данным в файле backend.

**6. Сборка и запуск контейнера**

    cd..
    docker-compose -f docker-compose.prod.yml up -d --build
>Подключитесь к контейнеру php-fpm (docker exec -it название_контейнера bash) и выполните миграцию (только при первом развертывании):

    php artisan migrate --seed
**7. Вход в систему**
>Приложение будет доступно на порту, указанном в docker-compose.prod.yml. <br/>Чтобы войти в админ-панель, добавьте к адресу /admin/login. Логин и пароль по умолчанию:

    admin@mail.ru
    123123

## Настройка через NPM (Nginx Proxy Manager)

> При настройке Frontend и Backend через Nginx Proxy Manager настоятельно рекомендуется указать параметры **SANCTUM_STATEFUL_DOMAINS** и **SESSION_DOMAIN** на этапе первоначальной настройки. Кроме того, в настройках NPM необходимо добавить следующие параметры:

    proxy_set_header X-XSRF-TOKEN $cookie_XSRF_TOKEN;
    proxy_set_header Host              $host;
    proxy_set_header X-Forwarded-Host  $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
<img width="520" height="633" alt="изображение" src="https://github.com/user-attachments/assets/368b36e2-d4c3-4d8e-b578-d0d8ab553506" />
