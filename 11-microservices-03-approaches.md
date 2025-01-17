# Домашнее задание к занятию «Микросервисы: подходы»

Вы работаете в крупной компании, которая строит систему на основе микросервисной архитектуры.
Вам как DevOps-специалисту необходимо выдвинуть предложение по организации инфраструктуры для разработки и эксплуатации.


## Задача 1: Обеспечить разработку

Предложите решение для обеспечения процесса разработки: хранение исходного кода, непрерывная интеграция и непрерывная поставка. 
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- облачная система;
- система контроля версий Git;
- репозиторий на каждый сервис;
- запуск сборки по событию из системы контроля версий;
- запуск сборки по кнопке с указанием параметров;
- возможность привязать настройки к каждой сборке;
- возможность создания шаблонов для различных конфигураций сборок;
- возможность безопасного хранения секретных данных (пароли, ключи доступа);
- несколько конфигураций для сборки из одного репозитория;
- кастомные шаги при сборке;
- собственные докер-образы для сборки проектов;
- возможность развернуть агентов сборки на собственных серверах;
- возможность параллельного запуска нескольких сборок;
- возможность параллельного запуска тестов.

Обоснуйте свой выбор.

## Ответ:

Есть множество решений, таких как Gitlab, TeamCity, Jenkins. Я остановлю свой выбор на Gitlab.   
Расширения - Gitlab CI/CD — готовая система, в которой есть всё для выкатки кода в прод.   
Востребованность - его популярность бесспорно растёт, отчасти это связано с тем, что полезный функционал, который был платным, начали перетаскивать в бесплатную комьюнити-версию.   
Средства для отслеживания проблем - GitLab CI/CD позволяет выполнять параллельное тестирование различных веток кода. Результаты испытаний удобно анализировать в интерфейсе системы — вы всегда можете зайти и посмотреть, как прошёл билд.   
Ограничение доступа к репозиториям - в Jenkins вам приходится отдельно разграничивать доступ. В GitLab CI/CD  тем, кто совместно работает над проектом, вы можете назначать права, соответствующие их ролям. Это особенно актуально для корпоративных проектов.   
Весь запрашиваемый функционал реализован в Gitlab.

## Задача 2: Логи

Предложите решение для обеспечения сбора и анализа логов сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор логов в центральное хранилище со всех хостов, обслуживающих систему;
- минимальные требования к приложениям, сбор логов из stdout;
- гарантированная доставка логов до центрального хранилища;
- обеспечение поиска и фильтрации по записям логов;
- обеспечение пользовательского интерфейса с возможностью предоставления доступа разработчикам для поиска по записям логов;
- возможность дать ссылку на сохранённый поиск по записям логов.

Обоснуйте свой выбор.

## Ответ:
ELK stack - Этот набор компонентов обеспечивает удобное централизованное логирование (ведение журналов) с разных серверов. ELK stack позволяет надежно и безопасно получать данные из любого источника во всех форматах и работать с этими данными: осуществлять поиск по ним, анализировать и визуализировать их в режиме real-time (NRT).      

Elasticsearch — сердце стека ELK. Это распределенная RESTful-система на основе JSON, которая сочетает в себе функции NoSQL-базы данных (сохраняет все собранные данные), поисковой системы и аналитической системы.   

Logstash в стеке ELK представляет собой конвейер по парсингу данных (логов событий) одновременно из множества источников ввода и их обработки для дальнейшего использования в Elasticsearch. С помощью этой утилиты в сообщениях системных событий можно выделять поля и их значения, фильтровать и редактировать данные. Настраивается она через конфигурационные файлы.   

Kibana  — это web-панель для работы с логами, расширяемый пользовательский интерфейс. Он позволяет визуализировать проиндексированные данные в системе Elasticsearch в виде графиков и диаграмм.

## Задача 3: Мониторинг

Предложите решение для обеспечения сбора и анализа состояния хостов и сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор метрик со всех хостов, обслуживающих систему;
- сбор метрик состояния ресурсов хостов: CPU, RAM, HDD, Network;
- сбор метрик потребляемых ресурсов для каждого сервиса: CPU, RAM, HDD, Network;
- сбор метрик, специфичных для каждого сервиса;
- пользовательский интерфейс с возможностью делать запросы и агрегировать информацию;
- пользовательский интерфейс с возможностью настраивать различные панели для отслеживания состояния системы.

Обоснуйте свой выбор.

Zabbix - это универсальный инструмент мониторинга, способный отслеживать динамику работы серверов и сетевого оборудования, быстро реагировать на внештатные ситуации и предупреждать возможные проблемы с нагрузкой. Система мониторинга Zabbix может собирать статистику в указанной рабочей среде и действовать в определенных случаях заданным образом.   

Prometheus и Grafana 

Prometheus — это база данных временных рядов, Prometheus извлекает метрики через HTTP-вызовы к определенным конечным точкам, указанным в конфигурации Prometheus.

Grafana — это платформа с открытым исходным кодом для визуализации, мониторинга и анализа данных.

## Задача 4: Логи * (необязательная)

Продолжить работу по задаче API Gateway: сервисы, используемые в задаче, пишут логи в stdout. 

Добавить в систему сервисы для сбора логов Vector + ElasticSearch + Kibana со всех сервисов, обеспечивающих работу API.

### Результат выполнения: 

docker compose файл, запустив который можно перейти по адресу http://localhost:8081, по которому доступна Kibana.
Логин в Kibana должен быть admin, пароль qwerty123456.


## Задача 5: Мониторинг * (необязательная)

Продолжить работу по задаче API Gateway: сервисы, используемые в задаче, предоставляют набор метрик в формате prometheus:

- сервис security по адресу /metrics,
- сервис uploader по адресу /metrics,
- сервис storage (minio) по адресу /minio/v2/metrics/cluster.

Добавить в систему сервисы для сбора метрик (Prometheus и Grafana) со всех сервисов, обеспечивающих работу API.
Построить в Graphana dashboard, показывающий распределение запросов по сервисам.

### Результат выполнения: 

docker compose файл, запустив который можно перейти по адресу http://localhost:8081, по которому доступна Grafana с настроенным Dashboard.
Логин в Grafana должен быть admin, пароль qwerty123456.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
