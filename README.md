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

НАгло присваиваем себе право владения на эту штуку

![image](https://github.com/user-attachments/assets/5dd83713-e509-4247-bcc9-b1934c49e9e9)
