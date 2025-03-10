Первым делом нагло заимствуем образ Oracle Linux у преподавателя и используем его для того чтобы поднять ВМку.

Как только мы получили желанный образ ставим следущее `Выделяем 2+ ядер. Выделяем 4096+ МБ оперативы.` ` AHTUNG!!! СТАВИМ АНГЛИЙСКИЙ ПРИ УСТАНОВКЕ`

![image](https://github.com/user-attachments/assets/3061c7d7-2e51-4877-ab78-3d4fe968878f)
![image](https://github.com/user-attachments/assets/d9ba4d62-dd58-43d7-b67d-5b87f5c9ae06)

Когда вы наконец зашли в вашу чудесную ВМ открываем Терминал и начинаем ставить docker с использованием grafana при помощи следущих команд:

1. `sudo yum install wget`

Эта штука ставит утилитку на ВМку

![image](https://github.com/user-attachments/assets/5c730c48-9b71-44cd-83ac-3566b93c005f)

2. `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

Скачивает файл репозитория

![image](https://github.com/user-attachments/assets/10afb566-6d14-431d-892f-c46a16e9906b)

3. `sudo yum install docker-ce docker-ce-cli containerd.io`

Стввим docker:

![image](https://github.com/user-attachments/assets/3bd0cfc8-f1b3-44aa-aaf9-a4d54d367fe3)

![image](https://github.com/user-attachments/assets/34987ce4-9990-40b1-bc1f-906351f0fb89)

![image](https://github.com/user-attachments/assets/629d053b-8901-45ab-9487-bf51c61ac82e)

4. `sudo systemctl enable docker --now`
   
Запускаем эту прелесть и даем ему право на автозагрузку

![image](https://github.com/user-attachments/assets/108cf099-154e-4df1-bacc-61282cf7b462)

5. `sudo yum install curl`
   
Cмотрим есть ли у нас пакетик curl

![image](https://github.com/user-attachments/assets/0f06b9a0-557e-4167-953c-0d62814ce192)

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Объявление переменной COMVER, которую мы получили в результате curl запроса, эта штука хранит в себе номер последней версии Docker Compose `AHTUNG!!! НЕ ПОВТОРЯТЕ МОЕЙ ОШИБКИ ИСПОЛЬЗУЙТЕ СРАЗУ '' ЭТИ КОВЫЧКИ А НЕ КОТОРЫЕ НА КНОПКЕ С БУКВОЙ "Ё" Я ПОЛ ЧАСА СИДЕЛ ТУПИЛ ПОЧЕМУ НЕ РАБОТАЕТ`

![image](https://github.com/user-attachments/assets/94fee561-87b4-4fcd-abf1-efb84ef0db6a)

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-aarch64 -o /usr/bin/docker-compose`
Качаем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

`ACHTUNG!!! СМОТРИМ НА ВЕРСИЮ АКТУАЛЬНУЮ РУЧКАМИ НА ГИТХАБЕ ИНАЧЕ НЕ СКАЧАЕТСЯ НИЧЕГО. ТУТ БУДЕТ v2.33.1 https://github.com/docker/compose/releases/ <--- АКТУАЛОЧКА`

![image](https://github.com/user-attachments/assets/08b1974d-9480-4d32-ae30-a5452b000b6d)

8. `sudo chmod +x /usr/bin/docker-compose`

Даем права на выполнение файла docker-compose.

![image](https://github.com/user-attachments/assets/a3eca625-8a53-4c61-9581-0336bdc96ad6)

9. `docker-compose --version`
    
Проверка установленной версии Docker Compose.


