# Highload
homework №2

### 1. Выбор темы
* Сервис (Tiktok) для использования на территории Индии

### 2. Определение возможного диапазона нагрузок
* Tiktok ориентируется на мобильных пользователей, для этого расчитаем общее 
  число пользователей использующий мобильный интернет в Индии.
  
  * Общее число пользователей интернет в Индии на 2020 ~(650 000 000). Пруфы:
    [1.](https://www.cia.gov/library/publications/the-world-factbook/fields/204rank.html#AQ)
    [2.](https://www.internetlivestats.com/internet-users/india/)
    [3.](https://www.statista.com/statistics/255146/number-of-internet-users-in-india/)
	
  * Число пользователей, использующих мобильный интернет в Индии на 2020 составляет ~70% 
    от общего числа пользователей сети интернет в Индии ~(450 000 000). Пруфы:
    [1.](https://www.statista.com/statistics/558610/number-of-mobile-internet-user-in-india/)
    [2.](https://ourworldindata.org/internet)
	
* Число пользователей ~(450 000 000) является максимальной оценкой рынка для любого мобильного приложения в Индии.
  В этом числе не учитывается распределение целевой аудитории. Можно предположить, целивая аудитория Tiktok в 
  Индии раполагается в интервале от 18 до 44 лет. Для числинной оцеки объективной аудитории найдём распределение 
  пользователей сети интернет в мире по возрастным группам и предположим, что для Индии в среднем этот показатель идентичен.

  * Распределение пользователей сети интернет в мире по возрастным группам. Пруфы:
    [1.](https://www.statista.com/statistics/272365/age-distribution-of-internet-users-worldwide/)
    [2.](https://sproutsocial.com/insights/new-social-media-demographics/)
    [3.](https://telesputnik.ru/materials/trends/news/auditoriya-tiktok-v-rossii-dostigla-20-2-mln-polzovateley/)

    | Age range | Percent |
    | ----------|-------: |
    |  18 - 24  |  ~ 18%  |
    |  25 - 34  |  ~ 32%  |
    |  35 - 44  |  ~ 19%  |
    |  45 - 54  |  ~ 14%  |
    |  55 - 64  |  ~ 10%  |
    |  65 +     |  ~ 7%   |

* Заметим, что целевая аудитория составляет около 70% от общего кол-ва пользователей,
  использующих мобильный интернет в Индии. И соответственно это число можно оценить в ~(315 000 000)

### 3. Выбор планируемой нагрузки
* Положим среднюю нагрузку равной 40% от оцененной целевой аудитории ~(120 000 000) Пруфы: [1.](https://blog.hootsuite.com/what-is-tiktok/)

* В среднем активные пользователи тикток проводят 60 минут в приложении один за день. Пруфы: [1.](https://www.businessofapps.com/data/tik-tok-statistics/) [2.](https://www.oberlo.com/blog/tik-tok-statistics) 
[3.](https://www.theverge.com/interface/2020/6/10/21285309/tiktok-2020-user-numbers-revenue-smash-hit-mea-culpa )

* За 10 минут пользования сайтом, было использовано 230MB трафика и было сделанно 519 запросов.

	|                   |  Трафик | Колличество запросов |
	|-------------------|---------|----------------------|
	| Статика медиа     |  220 MB |          86          |
	| Остальная статика |  9 MB   |          209         |
	| Динамика          |  850 KB |          224         |

* За сутки пользования сервисом в среднем пользователем будет израсходованно:

	|                   | Трафик  | Колличество запросов |
	|-------------------|---------|----------------------|
	| Статика медиа     | 1320 MB |         516          |
	| Остальная статика | 54 MB   |         1254         |
	| Динамика          | 6 MB    |         1344         |

* Пруфы: [1.](1.1.png) [2.](2.2.png) [3.](3.3.png)

* Расчитаем средний трафик для динамики и статики:
	* Динамика: (6MB * 120 000 000) / (24 * 60 * 60) * 8 = 65 Gbit/S
	* Статика медиа: (1320MB * 120 000 000) / (24 * 60 * 60) * 8 = 14 Tbit/S
	* Остальная статика: (54MB * 120 000 000) / (24 * 60 * 60) * 8 = 0.6 Tbit/S
	
* Расчитаем средний RPS для динамики и статики:
	* Динамика: (1344 * 120 000 000) / (24 * 60 * 60) = 1 900 000 RPS
	* Статика медиа: (516 * 120 000 000) / (24 * 60 * 60) = 750 000 RPS
	* Остальная статика: (1254 * 120 000 000) / (24 * 60 * 60) = 1 800 000 RPS
	
* Итог:	

	|                   |   Трафик   |    RPS    |
	|-------------------|------------|---------- |
	| Статика медиа     | 14 Tbit/S  | 750 000   |
	| Остальная статика | 0.6 Tbit/S | 1 800 000 |
	| Динамика          | 65 Gbit/S  | 1 900 000 |
	
* Отдельно стоит учитывать, что нагрузка распределенна не равномерно, её распределение зависит от времени суток. Из проведённого исследования [1.](http://ceur-ws.org/Vol-2353/paper71.pdf) можно гурбо оценить, что ночная нагрузка меньше средней нагрузки в ~2 раза, а дневная больше средней в ~3 раза.  

### 4. Логическая схема базы данных
* Выделим основные сущности в нашем проекте: пользователь, видео, подписка, лайк, тег и коментарий. На рисунке отображены поля моделей и заданы отношения между каждой из моделей. 

![bd_scheme](bd_scheme.png)

* Выделим основные сервисы приложения:

![service_schema](services_diagram.png)

### 5. Физическая системы хранения
* Рассмотрим сервисы приложения и выделим характеристики физических систем хранения:
	* Account service - Хранит данные пользователя. Среднее чтение, средняя запись, хранение "холодных данных", повышенные требования к сохранности информации.
	
	* Autorization service - Авторизует пользователя. Не большой объём данных. Частое чтение, частая запись, хранение "горячих данных".
	
	* Session service - Возвращяет id пользователя, по его сесии. Не большой объём данных. Частое чтение, частая запись, хранение "горячих данных".
	
	* Likes Service - Позволяет пользователю ставить лайки. Не большой объём данных. Частое чтение, частая запись, хранение "горячих и холодных" данных. Конкурентный доступ
	
	* Subscription Service - Позволяет пользователю подписываться на авторов. Не большой объём данных. среднее чтение, редкая запись, хранение "горячих и холодных" данных.
	
	* Comment Service - Позволяет пользователю оставлять коментарии к видео. Хороший объём данных. среднее чтение, редкая запись, хранение "горячих и холодных" данных.
	
	* Tag service - Позволяет получать группы видео по тегам. Хороший объём данных. Частое чтение, частая запись, хранение "горячих" данных.
	
	* Media service - Позволяет загрузить конкретное видео. Большой объём хранимой информации, частое чтение, редкая запись

* Для хранения большого объёма медиа данных лучше всего использовать файловую систему, так как не требуется корректная обработка конкурентного изменения данных. Преимуществом такого подхода является его относительно лёгкое расширение на большое колличество физических серверов.

* Для хранения данных пользователя, коментариев и тегов будем использовать Postgress. По сравнению с другими реалиционными базами данных он имеет, поддержку баз данных неограниченного размера, мощные и надёжные механизмы транзакций и репликации. Имеет хорошую производительность при аналитических запросах. 

* Для хранения активных сессий пользователя, лайков и подписок будем использовать Redis + Memcached с записью "холодных" данных на диск.

### 6. Выбор прочих технологий
* Языки программирования
	* Backend - Golang, C ++. Преимущества этих языков состоит в: 
		* Большом рынке программистов
		* Поддержке параллельных вычислений
		* Компилируемости
		* Статической типизации
		* Хорошей документационной базе

	* Frontend - Css, HTML , JavaScript, TypeScript, React , Sass, Webpack. 
		*React, обеспечивает модульность, быстрый рендеринг, высокую run-time производительность, работает с virtual DOM.

* Протоколы взаимодействия
	* Протокол связи между фронтендом и бэкендом - https, данные будут передаваться в формате json.

* Общение между микросервисами на бэкенде будет осуществляться по протоколу gRPC, данные будут передаваться в формате protobuf.

### 7. Расчет нагрузки и потребного оборудования
* Фронтенд. 
	* Статика без раздачи медиа.
		* Для отдачи статики будем использовать сервера с nginx.  
		* Примерно определим средний размер пакета 0.6 Tbit/S / 1 800 000 RPS = 354Kbit
		* Исходя из размера пакета и из документации nginx [1.](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) 
[2.](https://www.nginx.com/blog/nginx-websockets-performance/), можно сделать вывод, что для балансировки ~ 1 800 000 с 3х кратным запасом для пиковых нагрузок, то есть для 5 400 000 RPS для машины с конфигурацией: 
	
			|          CPU         |  Memory |   SSD   |
			|----------------------|---------|---------|
			|  2x Intel(R) 36 cores|  32 GB  |  256GB  |
	
			максимальный RPS, который будет приходиться на машину для http трафика составит не более 30 000. Таким образом потребуется 180 серверов.
	
	* Медиа статика
		* Для отдачи статики будем использовать сервера с nginx.
		* Определим необходимый объём хранилища медиа данных. Из статей [1.](https://www.oberlo.com/blog/tiktok-statistics) [2.](https://www.businessofapps.com/data/tik-tok-statistics/) [3.](https://influencermarketinghub.com/tiktok-stats/) можно сделать вывод, что пользователи будут загружать около 1 000 000 видео ежедневно, а также опираясь на то, что максимальный объём видео tictok составляет 75MB оценим объём данных с запасом на 5 лет 360 * 1 000 000 * 75 = 26PB.
		* Учитывая, что средняя скорость чтения с SSD диска ~700Mbit, то для покрытия нагрузки в 14Tbit с тройным запасом, то есть 42Tbit потребуется 42Tbit / 700Mbit = 63 000 дисков. Если в каждый сервер вмещается 64 диска, то минимальное число серверов 63 000 / 64 = 990.
		* Определим необходимый объём диска для хранения 26PB данных, с учётом двойного запаса. 52PB / 990 / 64 = 1TB
		* Рассмотрим так же оставшиеся критерии (CPS и пропускную способность)  для сервера с конфигурацией:
	
			|          CPU         | Memory  |    SSD    |
			|----------------------|---------|-----------|
			|  2x Intel(R) 8 cores | 2048 GB |  1TB x 64 |
			
		* Исходя из документации nginx [1.](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) 
[2.](https://www.nginx.com/blog/nginx-websockets-performance/) видно, что CPS для данного сервера ~10 000. Тогда CPS для 990 серверов равен 990 * 10 000 = 9 900 000CPS > 750 000, следовательно проблем с CPS нет. Пропускная способность для такого сервера ~70GBit, тогда общая пропускная способность 990 * 70Gbit = 67.5Tbit > 14Tbit * 3, следовательно с пропускной способностью всё в порядке. Таким образом получаем 990 серверов для отдачи медиа данных.
	
* Бэкенд.
	* Сервис данных пользователя 
		* А качестве сервера будем использовать nginx.
		* Максимальный объём данных записи одного пользователя можно с запасом оценить в 128KB, таким образом на 480 000 000 пользователей, с учётом роста понадобится 58TB.
		* Оценим RPS сервис авторизации. Исходя из того, что человек в стреднем проводит в приложении около 60 минут в день, а его сессия длиться около 5 минут, можно предположить, что за день он совершит 12 обращений к сервису. Таким образом можно оценить средний RPS для сервиса авторизации 12 * 120 000 000 / (60 * 24 * 24) = 16 800 RPS с учётом пиковых нарузок получим 50 400 RPS.
		* Оценивая максимальную производительность базы данных в 1000RPS на ядро получим, что потребуется 5 - 6 серверов с 32 ядрами.
		* Рассчитаем обём дискового пространства серверов 58TB / 6 = 10TB
		* Таким образом исходя из документации nginx [1.](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) [2.](https://www.nginx.com/blog/nginx-websockets-performance/), что будет достаточно 6 машин с конфигурацией:
		
			|          CPU         |  Memory  |    SSD     |
			|----------------------|----------|------------|
			| 2x Intel(R) 32 cores |  32 GB   | 512GB x 20 |

	* Сервис коментариев
		* Для отдачи данных будем использовать сервера с nginx.
		* Предположим, что под каждым новым видео роликом пользователи оставляют в среднем 10 коментариев и исходя из того, что каждый день на сервис заливается около 1 000 000 новых видео, а размер коментария максимально оценивается в 10KB, расчитаем необходимый дисковый объём c запасом на 2 года 1 000 000 * 10 * 10KB * 365 * 5 = 67TB
		* Оценим аналогично средний RPS 1 000 000 * 10 / (24 * 60 * 60) = 200RPS, с учётом пиковых нагрузок получим 600RPS
		* Оценивая максимальную производительность базы данных в 500RPS на ядро получим, что потребуется 3 - 4 сервера с учётом "запаса".
		* Таким образом исходя из документации nginx [1.](https://www.nginx.com/blog/testing-the-performance-of-nginx-and-nginx-plus-web-servers/) [2.](https://www.nginx.com/blog/nginx-websockets-performance/), что будет достаточно 4 машины с конфигурацией:
	
			|          CPU         |  Memory  |   SSD      |
			|----------------------|----------|------------|
			| 2x Intel(R) 32 cores |  16 GB   | 512GB x 32 |
		
	* 
	
### 8. Выбор хостинга / облачного провайдера и расположения серверов
* Для нашего сервиса воспользуемся облачным сервисом Amazon Web Services. [1.](https://aws.amazon.com/ru/about-aws/global-infrastructure/)

	* Для этого возьмем сервера в дата-центраx Мумбаи с 3 зонами доступности. [2.](https://aws.amazon.com/ru/about-aws/global-infrastructure/regions_az/) [3.](https://aws.amazon.com/cloudfront/features/)

	* В каждом регионе сервера будем брать из разных зон доступности, чтобы обеспечить отказоустойчивость в случае падения одного из дата-центров.

* Другие хостинги данного региона не обеспечивают необходимые вычислительные ресурсы.

### 9. Схема балансировки нагрузки (входящего трафика и внутрипроектного, терминация SSL)
* Балансировка нагрузки будет осуществляться с помощью Elastic Load Balancing. [1.](https://aws.amazon.com/ru/elasticloadbalancing/features/)
* Преимущества данного подхода заключаются в:
	* Высокой доступности - Elastic Load Balancing автоматически распределяет трафик по нескольким целевым объектам – инстансам Amazon EC2, контейнерам и IP‑адресам – в одной или нескольких зонах доступности.
	
	* Проверки работоспособности - Elastic Load Balancing может найти неисправные объекты, перестать отправлять им трафик, а затем распределить нагрузку среди оставшихся исправных объектов.
	
	* Возможности безопасности - С помощью облака Amazon Virtual Private Cloud (Amazon VPC) можно создавать группы безопасности, связанные с балансировщиками нагрузки, и управлять ими для обеспечения дополнительных возможностей, связанных с сетевой конфигурацией и безопасностью. Кроме того, можно создать внутренний (без выхода в Интернет) балансировщик нагрузки.
	
	* Терминации TLS - Elastic Load Balancing имеет встроенные возможности SSL/TLS‑расшифровки и управления сертификатами, что позволяет гибко и централизованно управлять настройками SSL на балансировщике нагрузки, экономя ресурсы ЦП для рабочего приложения.
	
	* Мониторинге в процессе работы - Для мониторинга производительности приложений в режиме реального времени Elastic Load Balancing поддерживает интеграцию с метриками Amazon CloudWatch и дает возможность отслеживать запросы средствами этого сервиса.

### 10. Обеспечение отказоустойчивости
* Использование Amazon Elastic Load Balancing

* Использование 3х зон доступности Amazon Web Services в Мумбаи

* Использование микросервисной архитектуры

* Использоваине технологии RAID 10 для хранения данных пользователей и медиа информации
	* Эффективная ёмкось S * N / 2
	* Допустимое количество вышедших из строя дисков от 1 до N/2 дисков. Информация не потеряется, если выйдут из строя диски в пределах разных зеркал.
	* Надёжность / скорость чтения / скорость записи - (высокая / высокая / высокая)
