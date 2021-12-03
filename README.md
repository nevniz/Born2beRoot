# Born2beRoot
Этот проект помог лучше понять виртуализацию, системное администрирование и Linux.

В учебном проекте нужно было запустить сервер на операционной системе Debian или CentOS с определёнными настройками с помощью виртуальной машины. Я выбрал Debian. Здесь опишу основные моменты из задания. В качестве бонусов нужно установить базу данных, дополнительный сервис для сервера и запустить сайт на WordPress. Запрещено устанавливать графическую оболочку.

Полное описание задания:
[en.subject.pdf](https://github.com/nevniz/Born2beRoot/files/7649626/en.subject.pdf)

Настроить разделы диска.
-

С помощью LVM мы должны создать зашифрованные разделы. Для бонусной части нужны следующие разделы: корневая папка, раздел подкачки, домашние директории пользователей, изменяемые файлы, системные сервисы, логи и другие временные файлы.  

<img width="697" alt="Screen Shot 2021-12-03 at 3 39 31 PM" src="https://user-images.githubusercontent.com/93081927/144604087-299394df-9ce5-4440-997f-2c2bd83206f1.png">

Настроить SSH.
-

Сделать так, чтобы можно было подключиться через порт 4242 и нельзя было подключаться через root.

Настроить UFW.
-

В правилах UFW должны быть открыты только порт 4242 и порты, которые нужны для выполнения бонусной части. Он должен работать с запуском виртуальной машины.

Имя хоста и пользователя, работа с группами.
-

Именем хоста должен быть логин учащегося с окончанием 42. В моём случае — это llawrenc42. Нужно знать, как изменить имя хоста при защите.

Создать пользователя с логином учащегося.

Пользователя нужно добавить в группу «user42» и «sudo».

Настроить политику паролей.
-

1. Пароль должен меняться каждые 30 дней.
2. Новый пароль можно поставить только через 2 дня.
3. Пользователю отправляется напоминание об изменении пароля за 7 дней до истечения срока.
4. Пароль должен состоять из 10 символов.
5. Он должен содержать букву верхнего регистра и цифру. 
6. Он не должен содержать более 3 повторяющихся символов.
7. В пароле не должно быть имени пользователя.
8. Пароль должен содержать не менее 7 символов, которые не являются частью прежнего пароля. Это правило не применяется для root.

Настроить sudo.
-

1. Запрос sudo ограничено 3 попытками при вводе неправильного пароля. 
2. Должно выводиться сообщение об ошибке, при неправильном вводе пароля.
3. Каждое использование sudo должно логироваться в файле. Должны сохраняться вводимые и выводимые данные. Файл с логом должен сохраняться в `/var/log/sudo/`. 
4. Режим TTY включен. 
5. Пути использования sudo ограничены. Например: `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin`.

Настроить скрипт мониторинга системы.
-
При запуске системы, скрипт [monitoring.sh](https://github.com/nevniz/Born2beRoot/blob/main/monitoring.sh) должен каждые 10 минут отображать информацию о системе. Для этого используется cron.

<img width="949" alt="Screen Shot 2021-12-03 at 3 40 20 PM" src="https://user-images.githubusercontent.com/93081927/144604188-6289b3e2-89e5-4877-9b08-8b88b353ed5a.png">

Скрипт должен выводить:

1. Архитектуру операционной системы и версию её ядра.
2. Количество физических процессоров.
3. Количество виртуальных процессоров.
4. Количество доступной оперативной памяти и её использования в процентах.
5. Количество доступной памяти и её использование в процентах.
6. Использование процессора в процентах.
7. Дата и время последнего запуска.
8. Используется ли LVM или нет.
9. Количество активных соединений.
10. Количество пользователей, использующий сервер.
11. IPv4 и MAC адрес.
12. Количество команд использованных с помощью sudo.

Бонусная часть.
-

Установить сайт на WordPress с lighttpd, MariaDB и PHP.

<img width="1351" alt="Screen Shot 2021-12-03 at 3 36 00 PM" src="https://user-images.githubusercontent.com/93081927/144604251-4be193c8-b0a0-42e8-83bb-516014e0cd83.png">

Установить дополнительный сервис на выбор. NGINX и Apache2 запрещены.
