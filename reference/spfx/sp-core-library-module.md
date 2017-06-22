# <a name="sp-core-library-module"></a>Модуль sp-core-library



## <a name="classes"></a>Классы

| Класс    |  Описание |
|:-------------|:---------------|
| [`Environment`](./sp-core-library/environment.md)     | Этот класс содержит контекстную информацию о среде, в которой размещаются платформа и ее компоненты. |
| [`Guid`](./sp-core-library/guid.md)     | Этот класс представляет глобальный уникальный идентификатор, описанный в стандарте IETF RFC 4122. Входная строка нормализуется и проверяется, что позволяет упростить остальной код, работающий с идентификатором GUID. Этот класс также обеспечивает базовую поддержку создания псевдослучайного GUID. Однако следует помнить, что его уникальность зависит от функции браузера Math.random() и может не подходить для некоторых приложений. |
| [`Log`](./sp-core-library/log.md)     | Класс Log предоставляет статические методы для ведения журнала сообщений на различных уровнях (подробности, информация, предупреждение, ошибка) и с контекстной информацией. Контекстная информация помогает определить, какой компонент создал сообщения, делает сообщения полезными и позволяет фильтровать их. |
| [`RandomNumberGenerator`](./sp-core-library/randomnumbergenerator.md)     | Это версия класса IRandomNumberGenerator по умолчанию, которая просто вызывает функцию Math.random(). |
| [`ServiceKey`](./sp-core-library/servicekey.md)     | ServiceKey — это ключ поиска, используемый при вызове метода ServiceScope.consume() для получения зависимости. Кроме того, этот ключ определяет версию зависимости по умолчанию, которую автоматически создает корневая область, если зависимость не найдена. Указав версию по умолчанию, вы сможете безопасно добавлять новые зависимости, не нарушая работу компонентов, загруженных старым основным приложением (которое не предоставляет новую зависимость). |
| [`ServiceScope`](./sp-core-library/servicescope.md)     | Класс ServiceScope позволяет компонентам формально регистрировать и использовать зависимости ("службы"), а также регистрировать различные версии в разных областях. Это повышает модульность, так как компоненты сильнее отделяются от их зависимостей. Предположим, различным компонентам требуется доступ к экземпляру IPageManager. Мы могли бы создать единственный экземпляр PageManager (т. е. глобальную переменную), но в некоторых случаях это не сработает, например если потребуется создать всплывающее диалоговое окно, которому необходим второй экземпляр PageManager. Лучше добавить PageManager в качестве параметра конструктора для каждого компонента, которому он необходим. Однако при этом сразу возникнет проблема, так как любому коду, вызывающему эти конструкторы, также необходим параметр PageManager. В приложении с большим количеством таких зависимостей бизнес-логика, которая связывает воедино много подсистем, со временем подберет параметр конструктора для каждой возможной зависимости, что неудобно. Очевидное решение — переместить все зависимости в класс с именем вроде ApplicationContext, а затем передавать его в качестве параметра конструктора. Это позволяет передавать параметр PageManager соответствующим классам, не загромождая классы-посредники. Однако у такой схемы есть один недостаток: у класса ApplicationContext есть жестко заданные зависимости от множества несвязанных элементов. Удобнее сделать его словарем, который может искать элементы для пользователей и поставщиков, которым известен правильный ключ поиска (т. е. ServiceKey). Это популярный конструктивный шаблон "указателя служб", знакомый нам по API SPContext из классического SharePoint. Класс ServiceScope развивает эту идею в двух основных направлениях: Во-первых, он предоставляет механизм определения области. Например, две разные страницы могут использовать уникальные экземпляры PageManager, совместно используя остальные общие зависимости. Во-вторых, он позволяет объекту ServiceKey предоставлять версию зависимости по умолчанию. Это важно для стабильной работы API в нашей модульной клиентской среде: Предположим, в версии 2.0 нашего приложения появился новый интерфейс IDiagnosticTracing, который потребуется компоненту версии 2.0. Приложению версии 1.0 не удастся загрузить компонент версии 2.0. Можно потребовать, чтобы каждый пользователь проверял приложение на отсутствие зависимостей и обрабатывал такие случаи, но для этого потребуется много проверок. Лучше обеспечить наличие версии по умолчанию. Это может быть тривиальное поведение, которое упростит работу компонентов. Использование: экземпляры ServiceScope создаются с помощью метода ServiceScope.startNewRoot() или ServiceScope.startNewChild(). Изначально они находятся в "незавершенном" состоянии, при котором можно вызывать метод provide() для регистрации ключей служб, но вызов метода consume() запрещен. После вызова метода ServiceScope.finish() вызывать метод consume() разрешено, а метод provide() — запрещено. Такая семантика гарантирует, что метод ServiceScope.consume() всегда возвращает для одного ключа один и тот же результат, не зависящий от порядка инициализации. Кроме того, она позволяет поддерживать циклические зависимости, не беспокоясь о бесконечных циклах даже при работе со внешними компонентами, реализованными третьими сторонами. Чтобы избежать ошибок, рекомендуем всегда вызывать метод consume() в функции обратного вызова из метода serviceScope.whenFinished(). |
| [`TimeProvider`](./sp-core-library/timeprovider.md)     | Это версия класса ITimeProvider по умолчанию, которая просто вызывает фактические API браузера. |
| [`UrlQueryParameterCollection`](./sp-core-library/urlqueryparametercollection.md)     | Класс для хранения и извлечения параметров запросов. URL-адрес можно указывать относительно сервера, а пустые и нулевые строки будут анализироваться. Первый параметр запроса должен начинаться с символа ?, а все последующие — с символа &. Кроме того, этот класс поддерживает фрагменты. Поведение в крайних случаях: при пустом значении (www.example.com/?test=) сохраняются ключ и пустое значение; если в queryParam нет знаков равенства (www.example.com/?test), сохраняются ключ и неопределенное значение; при пустом queryParam (www.example.com/?&debug=on) сохраняются неопределенные ключ и значение; если параметр запроса содержит только знаки равенства (www.example.com/?=&debug=on), сохраняются пустые ключ и значение строки. |
| [`UrlUtilities`](./sp-core-library/urlutilities.md)     | Распространенные вспомогательные функции для работы с URL-адресами. Эти служебные программы отличаются простотой, небольшим размером и широкими возможностями применения. |
| [`Validate`](./sp-core-library/validate.md)     | Этот класс обеспечивает стандартный способ проверки свойств и параметров функций. В отличие от утверждений отладки, проверки Validate всегда выполняются и всегда возвращают ошибку, даже в рабочей версии. Не злоупотребляйте этими проверками, так как это может повлиять на производительность. |
| [`Version`](./sp-core-library/version.md)     | Этот класс представляет версии в строковом формате MAJOR.MINOR[.PATCH[.REVISION]], где MAJOR, MINOR, PATCH и REVISION — это целые числа. Параметры PATCH и REVISION — необязательные. Значения могут начинаться с нуля, но это никак не влияет на сравнение. Примеры: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004 |



## <a name="interfaces"></a>Интерфейсы

| Интерфейс    |  Описание |
|:-------------|:---------------|
| [`IRandomNumberGenerator`](./sp-core-library/irandomnumbergenerator.md)   | Это интерфейс ServiceScope, который позволяет модульным тестам предоставлять детерминированный источник псевдослучайных чисел.  |
| [`IServiceCollection`](./sp-core-library/iservicecollection.md)   | Сокращенный шаблон для извлечения известных служб из объекта ServiceScope.  |
| [`ITimeProvider`](./sp-core-library/itimeprovider.md)   | Это интерфейс ServiceScope, который позволяет модульным тестам имитировать системные часы.  |



## <a name="enumerations"></a>Перечисления

| Перечисление      | Описание|
|:-----------|:------------|
|[`DisplayMode`](./sp-core-library/displaymode.md)    | DisplayMode обозначает режим отображения страницы и/или ее содержимого (например, текста и веб-частей). |
|[`EnvironmentType`](./sp-core-library/environmenttype.md)    | Перечисление, описывающее тип среды, в которой работает платформа. |



