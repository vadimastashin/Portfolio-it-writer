# Apache открыл доступ к предварительной версии Spark 1.6.0

22 ноября 2015 года стал доступен для предварительного ознакомления релиз новой версии популярного фреймворка Apache Spark 1.6.0. Продукт с самого начала получил лестные отзывы разработчиков и крупных компаний-клиентов. О поддержке фреймворка в той или иной форме заявили такие известные гиганты ИТ-индустрии, как IBM, Microsoft и многие другие.

## Краткая история проекта

История Apache Spark хорошо известна, однако для понимания некоторых деталей стоит кратко рассказать об основных этапах развития проекта. Возникновение идеи фреймоворка для работы с большими данными относится к 2009 году. Spark появился в недрах одной из самых известных лабораторий Калифорнийского университета (Беркли) AMPLab[1].

Изначально фреймворк был исследовательским проектом[2], но через год обрел статус программного продукта с открытым исходным кодом. В результате, на GitHub появился доступный для заинтересованных лиц и компаний код  фреймворка, стало быстро создаваться сообщество разработчиков Spark. В 2013 году Spark переехал под крыло Apache, и в сентябре того же года разработчики предоставили доступ к версии Spark 0.8.0 с поддержкой YARN[3].

К тому моменту Spark сумел обрести широкую поддержку разработчиков и заинтересованных компаний. Об этом самым наглядным образом говорят итоги Саммита Spark, проведенного накануне релиза версии 0.8.1 [вышла 19 декабря 2013 года](4). По информации организаторов, в мероприятии приняли участие более 450 разработчиков из 13 стран. Более 180 компаний уже на тот момент выразили заинтересованность использовать новый фреймворк[5].

Spark оказался крайне востребованным продуктом, однако, как и многие проекты подобного рода, не был лишен ряда недостатков. За октябрь-ноябрь 2015 года вышло два обновления фреймворка: 2 октября  - Spark 1.5.1[6], 9 ноября – версия 1.5.2[7]. Оба обновления, как следует из анонса разработчиков, потребовались для решения различных проблем, обнаруженных в работе фрейморка.

Use cases + images:

## Новая версия - преодоление старых проблем фреймворка

Выход новой версии также потребовался в связи с жалобами разработчиков и пользователей на главную проблему, обнаруженную в предыдущих версиях фреймворка. Речь идет об управлении памятью. Поэтому в ответ на критику недостатков старых версий авторами предварительного релиза уже заявлено, что Spark  1.6 станет более эффективным[8].

Для того, чтобы заинтересованные лица убедились в этом, компания Databricks[9] - один из главных разработчиков и провайдер облачной платформы для создания и запуска приложений Spark – предложил протестировать предварительную версию Spark 1.6 на своем сайте[10]. Код также можно скачать прямо с с сайта Apache[11]. Здесь же подробно затронут вопрос о ключевых обновлениях фреймворка.

## Основные нововведения

Предлагаемая новая версия содержит, в основном, серьезные изменения[12] в методах управления памятью. В более ранних версиях Spark доступная память распределялась на два раздела: один для данных и второй для выполнения. Это требовало от пользователей понимания того, сколько памяти нужно выделить для каждого из них, как правильно распределить память. Возможно, именно эта особенность вызвала жалобы пользователей[13] на неудобное управление памятью.

В версии 1.6 память для работы с данными (execution memory) и память для хранения данных (storage memory) могут занимать дополнительный объем друг у друга в зависимости от обстоятельств. На практике это значит, что для многих приложений станет доступным значительное увеличение памяти. А это можно использовать для операторов (operators), например, соединений (joins) и агрегирования (aggregations).

Тем не менее, в предлагаемой версии остается несколько ограничений. В то время как дополнительная память для работы с данными может быть позаимствована при необходимости, дополнительная занимаемая память для хранения данных никогда не освобождается. Для обеспечения обратной совместимости 1.6 также включает в себя унаследованный режим управления жестко разделенной (fixed-partition memory management mode).

Версия 1.6 также продолжает работу версии 1.5 с проектом Tungsten[14]. Этот проект представляет собой попытку переписать низкоуровневое управление Spark’ом памятью и процессором [rewrite Spark's low-level handling of memory and CPU](15). По мере увеличения эффективности и популярности Spark среди разработчиков, все больше его узких мест в производительности, как выясняется, вызваны ограничениями собственно виртуальной машины Java: такими, к примеру, как сборщик мусора (garbage collector).

## Удобство для пользователей - прежде всего

Еще одним ключевым дополнением к Spark 1.6 является Dataset API для работы с коллекциями типизированных объектов (collections of typed objects). Ранее пользователям Spark приходлось выбирать из двух API для взаимодействия с данными: RDD – то есть по существу коллекции нативных Java-объектов (RDDs, essentially collections of native Java objects)  (что было полезно, но медленно); и DataFrames, т.е. коллекциями структурированных бинарных данных (менее безопасные, но более быстрые) (DataFrames, collections of structured binary data (less safe, but faster).
Пакеты данных (datasets) объединили преимущества обоих: статическую типизацию (static typing) и пользовательские функции RDD (user functions of RDDs), проверку типов во время компиляции (compile-time type checking), а также лучшую производительность DataFrames. Пакеты данных (Datasets) и DataFrames также должны свободно взаимодействовать; библиотеки, которые принимают один тип данных, могут принимать также и другой
Компонент данных в реальном времени в Spark – Spark Streaming[16] – также получил значительный импульс (популярность), благодаря изменению в его состоянии отслеживания API (to its state-tracking API). Это делает его легче для программ, которые хранят большое количество информации о состоянии (state information) при использовании потоков (например, для пользовательских сессий), так что влияние на память меняется только с изменениями в этом состоянии, а не во всем размере состояния (rather than the entire size of the state). Компания-разработчик Databricks утверждает, что это может обеспечить улучшение в десять раз больше при некоторых рабочих нагрузках (workloads). Но поскольку у Spark Streaming остаются некоторые проблемы с производительностью[17], пользователи будут рады любым улучшениям.

Другие изменения нельзя назвать существенными, но знать о них будет полезно.  Среди них:

    - возможность устойчивой конвейерной обработки (persistent piplines) в Spark ML (таким образом можно приостановить или возобновить работы);
    - способность выполнять Spark SQL-запросы к неструктурированным файлам (flat files) в поддерживаемых форматах[18];
    - некоторые новых алгоритмов машинного обучения;
    - улучшения в R и Python API.

Последнее может помочь расширить горизонты для использования Spark. В то время как Python сохраняет ведущие позиции в качестве ведущего языка для науки и математики[19], поддержка API для этого языка в Spark традиционно отставала.

________________________________________
[1] <https://amplab.cs.berkeley.edu/>

[2] <http://spark.apache.org/research.html>

[3] <http://spark.apache.org/releases/spark-release-0-8-0.html>

[4] <http://spark.apache.org/releases/spark-release-0-8-1.html>

[5] <https://spark-summit.org/2013/>

[6] <http://spark.apache.org/news/spark-1-5-1-released.html>

[7] <http://spark.apache.org/news/spark-1-5-2-released.html>

[8] <https://www.mail-archive.com/dev@spark.apache.org/msg12111.html>

[9] <https://databricks.com>

[10] <https://databricks.com/blog/2015/11/20/announcing-spark-1-6-preview-in-databricks.html>

[11] <https://www.mail-archive.com/dev@spark.apache.org/msg12111.html>

[12] <https://issues.apache.org/jira/browse/SPARK-10000>

[13] <http://www.infoworld.com/article/3004460/application-development/5-things-we-hate-about-spark.html>

[14] <http://www.infoworld.com/article/2982475/big-data/spark-15-shows-mapreduce-the-exit.html>

[15] <https://issues.apache.org/jira/browse/SPARK-9697>

[16] <http://www.infoworld.com/article/2854894/application-development/spark-and-storm-for-real-time-computation.html>

[17] <http://www.infoworld.com/article/3004460/application-development/5-things-we-hate-about-spark.html>

[18] <https://docs.cloud.databricks.com/docs/spark/1.6/examples/query.files.sql.html>

[19] <http://www.infoworld.com/article/2949564/data-science/python-hadoop-project-data-scientists.html>
