# Настройка облачной инфраструктуры для проекта по определению мошеннических транзакций

### 0. Подготовка к работе

https://yandex.cloud/ru/docs/cli/quickstart#install

https://yandex.cloud/ru/docs/tutorials/infrastructure-management/terraform-quickstart

```
iex (New-Object System.Net.WebClient).DownloadString('https://storage.yandexcloud.net/yandexcloud-yc/install.ps1')
yc init
terraform init
```

### 1. Создать новый backet в Yandex Cloud Object Storage с использованием terraform скрипта. 

Содержимое terraform скрипта - ```./infrastructure```

### 2. Скопировать в него содержимое предоставленного Вам хранилища с использованием инструмента s3cmd. 

![S3](img/s3.PNG?raw=true "S3")

### 3. Создать Spark-кластер в Data Proc с двумя подкластерами

Содержимое terraform скрипта - ```./infrastructure```


### 4. Соединиться по SSH с мастер-узлом и выполнить на нём команду копирования содержимого хранилища

![hdfs](img/hdfs.PNG?raw=true "hdfs")

### 5. Пользуясь тарифным калькулятором Yandex Cloud, оценить месячные затраты

В тарифном калькуляторе отсутствует Data Proc =(

При просмотре запущенного кластера, цена Data Proc - 35,96₽ в час

S3 на 120Gb ~ 240 рублей в месяц

### 6. Предложить способы для оптимизации затрат на содержание Spark-кластера в облаке

Я заменил hetwork-ssd диски на network-hdd, тем самым снизил стоимость и обошел квоту в 200Gb на общий объем SSD к кластера.

Для S3 прописал класс хранилища на холодное.

Пока ублал Compute ноду, т.к. она не требовалась для задания.

Основной расход идет на CPU и RAM DataProc, при сокращении этих ресурсов можно заметно сэкономить. 

### 7. В соответствии с достигнутыми результатами, изменить статус ранее созданных задач.

https://github.com/users/BelAnt/projects/1/

### 8. Полностью удалить созданный кластер, чтобы избежать оплаты ресурсов в период его простаивания.

Удалил через ```terraform destroy -auto-approve```