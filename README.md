Первым делом нагло заимствуем образ Oracle Linux у преподавателя и используем его для того чтобы поднять ВМку.

Как только мы получили желанный образ ставим следущее `Выделяем 2+ ядер. Выделяем 4096+ МБ оперативы.` ` AHTUNG!!! СТАВИМ АНГЛИЙСКИЙ ПРИ УСТАНОВКЕ`

![image](https://github.com/user-attachments/assets/3061c7d7-2e51-4877-ab78-3d4fe968878f)
![image](https://github.com/user-attachments/assets/d9ba4d62-dd58-43d7-b67d-5b87f5c9ae06)

Когда вы наконец зашли в вашу чудесную ВМ открываем Терминал и начинаем ставить docker с использованием grafana при помощи следущих команд:

1. `sudo yum install wget` `sudo yum install curl`

Первая штука ставит утилитку на ВМку, а вторая грузит нам пакетик с Curl

![image](https://github.com/user-attachments/assets/b93a56a9-fbbf-4109-a965-93deb3a5722d)

2. `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

Скачивает файл репозитория

![image](https://github.com/user-attachments/assets/93749241-8898-42ed-a022-7bf4449777a7)


3. `sudo yum install docker-ce docker-ce-cli containerd.io`

Стввим docker:

![image](https://github.com/user-attachments/assets/adb6154e-c28b-411b-b38e-6b6dadd6ea8e)

![image](https://github.com/user-attachments/assets/87a9fa16-6727-429f-b2bd-bd6e37345708)


4. `sudo systemctl enable docker --now`
   
Запускаем эту прелесть и даем ему право на автозагрузку

![image](https://github.com/user-attachments/assets/e78faf4b-060c-4784-9caf-429cc2f13d84)

5. `sudo yum install curl`
   
Cмотрим есть ли у нас пакетик curl

![image](https://github.com/user-attachments/assets/0f06b9a0-557e-4167-953c-0d62814ce192)

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Объявление переменной COMVER, которую мы получили в результате curl запроса, эта штука хранит в себе номер последней версии Docker Compose `AHTUNG!!! НЕ ПОВТОРЯТЕ МОЕЙ ОШИБКИ ИСПОЛЬЗУЙТЕ СРАЗУ '' ЭТИ КОВЫЧКИ А НЕ КОТОРЫЕ НА КНОПКЕ С БУКВОЙ "Ё" Я ПОЛ ЧАСА СИДЕЛ ТУПИЛ ПОЧЕМУ НЕ РАБОТАЕТ`

![image](https://github.com/user-attachments/assets/7c2728d0-bee0-47b2-9aec-5a63d6e8929c)


7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`
   
Качаем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

![image](https://github.com/user-attachments/assets/d9fd331f-c0dd-4c1f-b475-5c797ab7b995)

8. `sudo chmod +x /usr/bin/docker-compose`

Даем права на выполнение файла docker-compose.

![image](https://github.com/user-attachments/assets/5b9c7ae4-e7ea-45e0-b9f9-12830ecaf460)

9. `docker --version`
    
![image](https://github.com/user-attachments/assets/9f89ca27-cde1-455f-9ba6-5c99b9912497)

Cмотрим какая у нас версия Docker Compose.

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

Клонируем репозиторий с github, содержащий Grafana

![image](https://github.com/user-attachments/assets/086b92b6-3973-46fa-aedc-29f67d7eff46)

11.`cd grafana_stack_for_docke`

Бежим в директорию (папку) где у нас сидит Grafana

![image](https://github.com/user-attachments/assets/f4d439d0-8f24-43a3-a281-16923fb151ee)

12. `sudo mkdir -p /mnt/common_volume/swarm/grafana/config`  `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

Делаем еще папки для Grafana

![image](https://github.com/user-attachments/assets/45abe381-b91e-41f2-b6b2-12702258d646)

13. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

Нагло присваиваем себе право владения на эту штуку

![image](https://github.com/user-attachments/assets/5dd83713-e509-4247-bcc9-b1934c49e9e9)

14. `touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

Делаем конфиг файл 

![image](https://github.com/user-attachments/assets/35d104b9-e5ec-4c9d-b927-349e030d5a25)

15. `cp config/* /mnt/common_volume/swarm/grafana/config/`

Копируем все файлы из папки config в /mnt/common_volume/swarm/grafana/config/

![image](https://github.com/user-attachments/assets/35e80b04-530f-4bd6-89c2-f73ac7aa8358)

16. `mv grafana.yaml docker-compose.yaml`

Переименовываем файл grafana.yaml в docker-compose.yaml

![image](https://github.com/user-attachments/assets/71c5bdfa-abb4-481c-b280-40bae62f0a39)

17. `sudo docker compose up -d`

Запускаем эту лошадку (надо будет подождать)

![image](https://github.com/user-attachments/assets/1c0b265f-dd51-48e6-8a86-37676a2e3b35)

![image](https://github.com/user-attachments/assets/1b1d3a43-fdf5-4a03-91a8-74a170e7f3b1)

IT'S ALIVE!!!

18. Бежим в Файерфокс и идем по адресу `localhost:3000`

![image](https://github.com/user-attachments/assets/27b2f843-f8e8-4a6f-a5dd-403e77c43f2c)

Там вводим логин с паролем 

Логин `admin`

Пароль `admin`

И там мы попадем на домашнюю страницу

![image](https://github.com/user-attachments/assets/169ef731-1bde-4edd-a8a5-fd35f22eb076)

19. `vi docker-compose.yaml`

Заходим в кофиг Docker 

![image](https://github.com/user-attachments/assets/6296c1b9-f821-4bad-96e9-ed5dbb82df97)

![image](https://github.com/user-attachments/assets/18a7b698-d341-49d9-88fd-e35bc2c6d19e)

![image](https://github.com/user-attachments/assets/6aff9d9c-017c-45af-a2c3-869fafdb9caf)

Чтобы выйти отсюда вводим команду `:wq`

20. `sudo docker compose up -d`

Запускаем Grafana

![image](https://github.com/user-attachments/assets/f2da311f-13f0-4b37-ac8a-a16d42921888)

21. `sudo docker compose stop`

Стопим Grafana

![image](https://github.com/user-attachments/assets/403c1e72-7e73-463e-b7e3-278ed2bda177)

22. `sudo docker compose down`

Полностью стопим Grafana

![image](https://github.com/user-attachments/assets/3e24f915-16f9-4bba-8143-dde34c7814e7)

PROMITEUS

23. `sudo git clone https://github.com/0minty/Grafana-Install.git`

Нагло копируем конфиг и потом с помощью `ls` смотрим все ли у нас поставилось

24. `cp docker-compose.yaml /home/ваш пользователь/grafana_stack_for_docker/`

Копируем конфиг Docker в папку Grafana

![image](https://github.com/user-attachments/assets/207ff0f7-e96f-4261-972a-b65cf6c1176b)

25. `cp prometeus.yaml /home/ваш пользователь/grafana_stack_for_docker/`

С Prometeus делаем то же самое

![image](https://github.com/user-attachments/assets/d1508368-1a92-4c7c-b0a3-d3a82760aef7)

26. `mv prometheus.yaml /mnt/common_volume/swarm/grafana/config`

Переносим конфигурационный файл prometheus.yaml в конфиг Grafana

27. `ls`

Смотрим все ли у нас поставилось куда надо 

![image](https://github.com/user-attachments/assets/cd1d6cfa-c7f9-478b-b0bf-919982f94833)

27. `sudo docker compose up -d`

Запускаем Docker на фоне 

![image](https://github.com/user-attachments/assets/bf28b6e3-8aa3-4ac8-8e1d-1a91945363ff)

28. Переходим на сайт `localhost:3000`

Пользователь и Пароль GRAFANA: `admin`

Код графаны: `3000`

Код прометеуса: `http://prometheus:9090`

В меню выбираем вкладку Dashboards и создаем Dashboard

Нажимаем кнопку +Добавить визуализацию, а затем «Настроить новый источник данных»

Выбираем Prometheus

![image](https://github.com/user-attachments/assets/ecdd34f3-d84c-454f-b33e-f034d4ce8328)

Заполняем данные в открывшемся окне

Пункт Connection

http://prometheus:9090

Пункт Authentication

Базовая аутентификация

Пользователь: admin

Пароль: admin

Нажимаем на Save & test и должно показывать зелёную галочку

![image](https://github.com/user-attachments/assets/db4d0fa9-d6f0-458f-80b8-e73f5d9b3b2f)

29. В меню выбираем вкладку Dashboards и создаем Dashboard

Тыкаем на кнопку "Import dashboard"

![image](https://github.com/user-attachments/assets/c879a399-0c2c-4de0-b009-82f6e91fedc8)

30. В пункт `Find and import dashboards for common applications at grafana.com/dashboards`: пишем 1860

![image](https://github.com/user-attachments/assets/0db8a1d9-26ae-48da-b50a-acaf3fbb3a8e)
