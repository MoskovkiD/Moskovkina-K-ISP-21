# Moskov
Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux
Выделить 2+ ядер.
Выделать 4096+ МБ оперативы.
При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке docker с использованием grafana, вводим следующий набор команд:

    sudo yum install wget

• устанавливает утилиту wget на вашу систему

![image](https://github.com/user-attachments/assets/b13eccb0-8996-4d1f-93cf-b634b174768a)


    sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

• Скачиваем файл репозитория

![image](https://github.com/user-attachments/assets/c1ba9304-973f-4258-b6ce-efddd3ee53e3)



    sudo yum install docker-ce docker-ce-cli containerd.io

• Устанавливаем docker

![image](https://github.com/user-attachments/assets/f6575da6-7bd4-45e3-8cfc-feb4665a547a)

![image](https://github.com/user-attachments/assets/a82d2a08-5081-49a0-846d-d786e723ee4a)


    sudo systemctl enable docker --now

• Запускаем его и разрешаем автозапуск

    sudo yum install curl

• Для этого сначала убедимся в наличие пакета curl

![image](https://github.com/user-attachments/assets/ef5c1edb-420c-41bb-9adc-fe0a5001d7ce)


    COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
    
• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней
версии Docker Compose

![image](https://github.com/user-attachments/assets/a212d420-efff-4b67-ab9b-eb2f15702cfa)



    sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
    
• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin


![image](https://github.com/user-attachments/assets/796389f9-6f71-451c-abaf-01ce3849a5fc)


    sudo chmod +x /usr/bin/docker-compose

• Предоставление прав на выполнение файла docker-compose.

    docker-compose --version

• Проверка установленной версии Docker Compose.

 ![image](https://github.com/user-attachments/assets/f2c2a072-9216-4bbb-9f5f-f83535269497)


• Можно скачать git прямо из командной строки прописав Y

    git clone https://github.com/skl256/grafana_stack_for_docker.git

• выдаст ошибку и предложит скачать git, согласиться и продолжить

![image](https://github.com/user-attachments/assets/4ab79cc4-a542-4fcc-bbc8-30dbd92243e8)


    cd grafana_stack_for_docker
    
• переход в папку

    sudo mkdir -p /mnt/common_volume/swarm/grafana/config

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

    sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

    sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

    touch /mnt/common_volume/grafana/grafana-config/grafana.ini

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

     cp config/* /mnt/common_volume/swarm/grafana/config/

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

    mv grafana.yaml docker-compose.yaml

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

    sudo docker compose up -d

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.

![image](https://github.com/user-attachments/assets/8b5c491f-6a2c-475b-963f-9771961575d9)


![image](https://github.com/user-attachments/assets/54b3c62e-9b1e-45b3-83b9-78cceb65cdea)


    sudo vi docker-compose.yaml

• Команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.

• Нас перекинет в текстовый редактор

• Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре

• Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services

![image](https://github.com/user-attachments/assets/469e5e00-f6b1-4c8f-99f6-cfcbf3914926)


    sudo vi prometheus.yaml
    
• команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.

• исправить targets: на exporter:9100,

![image](https://github.com/user-attachments/assets/f5f11aa0-873a-449b-b810-41d7939399e0)

![image](https://github.com/user-attachments/assets/f1f47c6a-ee5f-44c9-95f8-372c3ad79534)


## Grafana

![image](https://github.com/user-attachments/assets/88c472c3-1a61-4d6c-a631-af4af2492fc2)

* переходим на сайт `localhost:3000`
    * User & Password GRAFANA: `admin`
    * Код графаны: `3000`
    * Код прометеуса: `http://prometheus:9090

      
* в меню выбираем вкладку Dashboards и создаем Dashboard
  
![image](https://github.com/user-attachments/assets/5b31ff06-889d-48f3-9cbf-6219e34aa799)


* ждем кнопку +Add visualization, а после "Configure a new data source"
* выбираем Prometheus


![image](https://github.com/user-attachments/assets/aa3fed3a-c610-4934-9339-e38c054d2843)

* Connection
* `http://prometheus:9090`
  
![image](https://github.com/user-attachments/assets/8fe61438-3ff7-4f23-8deb-e55dbda8b83a)

* Authentication
    * Basic authentication
        * User: `admin`
        * Password: `admin`
        * Нажимаем на Save & test и должно показывать зелёную галочку
      
![image](https://github.com/user-attachments/assets/b1d8c747-66af-4a29-943a-b3a6c107fa5d)

* в меню выбираем вкладку Dashboards и создаем Dashboard
    * ждем кнопку "Import dashboard"
    * Find and import dashboards for common applications at grafana.com/dashboards: 1860 //ждем кнопку Load

      
![image](https://github.com/user-attachments/assets/d464ea90-b5d8-4d44-973d-028ce150a7a1)

 * Select Prometheus ждем кнопку "Import"

Возникла ошибка в графане, графан выдавал все по 00, после махинаций с кодами ниже все пришло в норму

![image](https://github.com/user-attachments/assets/d8f78757-ee0d-46a7-847c-fa510805f641)

Бум, результат

![image](https://github.com/user-attachments/assets/3b473d76-4c58-4a83-ab20-dda4bea9006d)


![image](https://github.com/user-attachments/assets/cbc36cb3-0984-49be-a86c-18dd2b3c277b)


![image](https://github.com/user-attachments/assets/b6bc7722-d2bb-4424-b565-44739424135b)


