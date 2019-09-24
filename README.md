# Level I
__*В:*__ Чем отличается Proc от lambda?  

__*О:*__ Что Proc, что лямда относятся к классу Proc, различий в них не так много, но они все же есть:   

 1. lambda чувствительна к количеству передаваемых аргументов, нежели Proc.  
 2. Если обернуть Proc и лямбду в функцию, то return прока прекратит выполнение функции, в случае с лямбдой функция продолжит выполняться.
---
__*В:*__ Чем отличается && от and?  

__*О:*__ Логически – ничем, так как означают логическое «И». Но в контексте языка Ruby они имеют разный приоритет в вызове. Так, and в приоритете стоит ниже, чем присваивание, поэтому стоит быть аккуратнее с этим.
___
__*В:*__ Какие плюсы и минусы Ruby по сравнению с другими современными языками программирования вы выделяете для себя?  

__*О:*__ Распишу по списку:  
* **Плюсы**  
    1. Изящный, визуально приятный и понятный для чтения синтаксис. Очень часто на stackoverflow встречал фразы вроде: `«Ruby is so elegant»`, и это действительно так.
    2. Понятная ООП модель. Всё – есть объект. Без множественного наследования и других спорных моментов этой парадигмы.
    3. Блоки, проки, лямбды, ```yield if block_given?, method_missing``` и т.д.
    4. Rails – на мой взгляд, самый сильный фреймворк для создания веб-приложений, где учтены многие моменты, облегчающие жизнь, начиная от скаффолдинга, заканчивая нативной CSRF защитой, экранированием и т.д. Это лидирующий фреймворк по числу коммитов, и многие фреймворки перенимают идеи у рельс.
    5. Метапрограммирование, можно в любой момент расширить существующий класс, переопределить стандартные методы и так далее. На курсах мы за несколько минут написали простой ретранслятор из Ruby в HTML, это было впечатляюще.
    6. Сообщество. Даже под узкоспециализированные вопросы, вроде ГИС (моя специальность в университете), есть свои решения и библиотеки. Добавить капчу от спама? – Есть гем, даже несколько. cron/background задачи? – Есть гем. Кейсов, где есть готовое решение, очень много.
    7. Соглашения вроде DRY, Convention over configuration, Thin controllers — fat models, а также отношение сообщества к код стайлу и поддержке чистоты своего кода.
 * **Минусы**  
    1. Разработка языка очень закрыта и поддерживается несколькими людьми. Это не очень хорошо, когда речь заходит об обновлениях, которые могут реализовать только большие компании. У того же Rails количество контрибьюторов сильно больше в сравнении с другими web-фреймворками, что позволяет ему быть передовым и конкурентоспособным.
    2. На данный момент отсутствует аннотация типов. Я использовал её в Python, это достаточно удобно, хоть и нагромождает код.
---
__*В:*__ В каком случае вы бы стали использовать Ruby on Rails для разработки web-приложения, а в каком — другой фреймворк?  

__*О:*__ Я бы не использовал RoR там, где ниша RoR и Ruby не занята. Например, ML, нейросети, Big Data, где де-факто является лидером Python. Также я бы не подключал RoR в простые веб-приложения, где, например, нужно сделать REST API + Swagger. Для этих задач будет достаточно легковесных решений, вроде Sinatra, Flask и т.д.
___
__*В:*__ Вы запустили большой и сложный ruby скрипт на вашем любимом дистрибутиве Linux, и в процессе работы он намертво «зависает». Как найти причину сбоя?  

__*О:*__ На моём опыте я решал это просто – через buybug и встроенный дебаггер в RubyMine. Дополнительно можно воспользоваться утилитой ps aux или htop, которая через grep нужного имени процесса покажет всю статистику и зависимости.
___
__*В:*__ Вы запустили большой и сложный ruby скрипт на вашем любимом дистрибутиве Linux, и в процессе работы он умирает, исчерпав память, хотя, казалось бы, не должен. Как найти причину сбоя?  

__*О:*__ Поскольку ruby – высокоуровневый язык, он не позволяет пользователю управлять памятью, использовать дестркуторы и т.д. Зато язык предоставляет библиотеки для бенчмарков, в которых уже можно проверить сколько памяти было использовано до/после вызова метода, после использования бенчмарков уже становится более ясно, в каком месте происходит утечка памяти.
___
__*В:*__ Некоторые проекты (Rails и не только) мы запускаем под JRuby. Как вы думаете, почему?  

__*О:*__ Я читал про то, как устроен интерпретатор-компилятор в Java, когда ещё интересовался разработкой под Android в школе. Думаю, что в JRuby удобнее работать с потоками, нежели в нативном Ruby. Возможно, в проекте нужны какие-либо наработки из Java. На своём опыте я сталкивался с подобными «гибридами» только когда переводил своё desktop-приложение на в машинный код и модули на C с помощью Cython. Делал это для того, чтобы усложнить reverse engineering кода.
___
__*В:*__ Какие плюсы и минусы библиотеки ActiveRecord в Rails вы знаете? Какие альтернативы существуют? В чем их плюсы и минусы? Какие из них вы использовали?  

__*О:*__ Библиотека ActiveRecord раскрывает одноимённый паттерн проектирования, а значит плюсы паттерна вроде «экземпляр класса – запись в таблице» можно отнести и к библиотеке. Из минусов очень популярен тот момент, когда сложные запросы приходятся писать на чистом SQL, но я лично с этим не сталкивался. Также существует другой паттерн под названием Data Mapper, в котором отделена логика сохранения модели в БД. Многие веб-фреймворки используют ActiveRecord в качестве дефолтного паттерна для обращение к БД, поэтому с альтернативами на практике я не знакомился.

# Level II
__*В:*__ Есть Rails приложение, развернутое на N серверах. В приложение нужно добавить загрузку и хранение аватаров.  

__*О:*__
1. Мне привычно использовать carrierwave.
2. По умолчанию carrierwave помещает загруженные файлы в папку uploads с названием модели. Для аватара путь будет выглядеть примерно так: uploads/user/avatar/1/sample.img. Для файлов лучше использовать файловую систему, так как это снижает нагрузку на БД.
3. Обычно фотографии просто обрезают по заданному формату, чтобы уменьшить место занимаемой фотографии на сервере. Также можно удалить метаданные.
4. Проверки лучше делать на клиентской и на серверной части. Обычно картинки ограничивают по размеру файла, по расширению (.jpeg, .jpg, .png), по заголовку (image) и по разрешению. С клиентской стороны я использовал bootstrap file input, также для AJAX загрузки хорошо подойдёт dropzoneJS. На серверной стороне пользовался встроенными валидациями в carrierwave и гемом на проверку размера файла.
5. Через файловую систему, урезанную в формате JPEG или Webp. В carrierwave для вывода изображения есть свои хелперы. Можно отдавать небольшие превью, а основную фотографию подгружать по запросу пользователя.
6. Дополнительно я реализовывал сохранение в кеше загружаемого файла, чтобы при ошибке валидации других моделей, изображение не исчезало с сервера и при повторном запросе его не пришлось снова загружать. Также часто требуется загрузить изображение удалённо по предоставленному URL, либо реализовать множественную загрузку изображений, сохранение в облачное хранилище. В carrierwave все эти моменты соблюдены и не вызывали каких-либо трудностей.
___
__*В:*__ Есть большое приложение с десятками тысяч тестов. Как лучше всего организовать код и тесты, чтобы добиться максимальной скорости прогона тестов?  

__*О:*__ Если нужно прогнать все десятки тысяч тестов, то стоит позаботиться о параллельном тестировании, которое сильно сократит общее время тестов. Параллельное тестирование нативно поддерживается в 6-ой версии Rails, в предыдущих версиях тоже есть дополнительные решения. Код прежде всего делится на категории тестирования: интеграционные, функциональные, системные и т.д. А дальше уже разбивается на тестирование различных бизнес-процессов, поведение пользователя, контроллеров, моделей, маршрутов, вьюх. И в зависимости от реализованных фич, проведённых изменений, мы можем запускать отдельные участки тестов, которые покроют нужный код.