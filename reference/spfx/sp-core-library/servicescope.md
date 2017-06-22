# <a name="servicescope-class"></a>Класс ServiceScope







Класс ServiceScope позволяет компонентам формально регистрировать и использовать зависимости ("службы"), а также регистрировать различные версии в разных областях. Это повышает модульность, так как компоненты сильнее отделяются от их зависимостей. Предположим, различным компонентам требуется доступ к экземпляру IPageManager. Мы могли бы создать единственный экземпляр PageManager (т. е. глобальную переменную), но в некоторых случаях это не сработает, например если потребуется создать всплывающее диалоговое окно, которому необходим второй экземпляр PageManager. Лучше добавить PageManager в качестве параметра конструктора для каждого компонента, которому он необходим. Однако при этом сразу возникнет проблема, так как любому коду, вызывающему эти конструкторы, также необходим параметр PageManager. В приложении с большим количеством таких зависимостей бизнес-логика, которая связывает воедино много подсистем, со временем подберет параметр конструктора для каждой возможной зависимости, что неудобно. Очевидное решение — переместить все зависимости в класс с именем вроде ApplicationContext, а затем передавать его в качестве параметра конструктора. Это позволяет передавать параметр PageManager соответствующим классам, не загромождая классы-посредники. Однако у такой схемы есть один недостаток: у класса ApplicationContext есть жестко заданные зависимости от множества несвязанных элементов. Удобнее сделать его словарем, который может искать элементы для пользователей и поставщиков, которым известен правильный ключ поиска (т. е. ServiceKey). Это популярный конструктивный шаблон "указателя служб", знакомый нам по API SPContext из классического SharePoint. Класс ServiceScope развивает эту идею в двух основных направлениях: Во-первых, он предоставляет механизм определения области. Например, две разные страницы могут использовать уникальные экземпляры PageManager, совместно используя остальные общие зависимости. Во-вторых, он позволяет объекту ServiceKey предоставлять версию зависимости по умолчанию. Это важно для стабильной работы API в нашей модульной клиентской среде: Предположим, в версии 2.0 нашего приложения появился новый интерфейс IDiagnosticTracing, который потребуется компоненту версии 2.0. Приложению версии 1.0 не удастся загрузить компонент версии 2.0. Можно потребовать, чтобы каждый пользователь проверял приложение на отсутствие зависимостей и обрабатывал такие случаи, но для этого потребуется много проверок. Лучше обеспечить наличие версии по умолчанию. Это может быть тривиальное поведение, которое упростит работу компонентов. Использование: экземпляры ServiceScope создаются с помощью метода ServiceScope.startNewRoot() или ServiceScope.startNewChild(). Изначально они находятся в "незавершенном" состоянии, при котором можно вызывать метод provide() для регистрации ключей служб, но вызов метода consume() запрещен. После вызова метода ServiceScope.finish() вызывать метод consume() разрешено, а метод provide() — запрещено. Такая семантика гарантирует, что метод ServiceScope.consume() всегда возвращает для одного ключа один и тот же результат, не зависящий от порядка инициализации. Кроме того, она позволяет поддерживать циклические зависимости, не беспокоясь о бесконечных циклах даже при работе со внешними компонентами, реализованными третьими сторонами. Чтобы избежать ошибок, рекомендуем всегда вызывать метод consume() в функции обратного вызова из метода serviceScope.whenFinished().


## <a name="constructor"></a>constructor
ЧАСТНЫЙ КОНСТРУКТОР — НЕ ВЫЗЫВАЙТЕ ЕГО ИЗ СВОЕГО КОДА.

**Подпись:** _constructor(parent: [ServiceScope](../sp-core-library/servicescope.md));_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет





## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`consume(serviceKey)`](consume-servicescope.md)     | `public` | `T` | Компоненты должны вызывать эту функцию для "использования" зависимости, т. е. поиска serviceKey и возвращения зарегистрированного экземпляра службы. Если найти экземпляр не удается, будет автоматически создан и зарегистрирован экземпляр по умолчанию с корневым объектом ServiceScope. |
|[`createAndProvide(serviceKey,simpleServiceClass)`](createandprovide-servicescope.md)     | `public` | `T` | Это сокращенная функция, эквивалентная созданию нового экземпляра simpleServiceClass и его регистрации с помощью метода ServiceScope.provide(). |
|[`createDefaultAndProvide(serviceKey)`](createdefaultandprovide-servicescope.md)     | `public` | `T` | Это сокращенная функция, которая создает реализацию по умолчанию для указанного объекта serviceKey, а затем регистрирует ее, вызывая метод ServiceScope.provide(). |
|[`finish()`](finish-servicescope.md)     | `public` | `void` | Сразу после создания объекта ServiceScope он находится в "незавершенном" состоянии, в котором разрешено вызывать метод provide(), но запрещено вызывать метод consume(). После вызова метода finish() метод consume() будет разрешен, а метод provide() — запрещен. Такой формализм полностью устраняет ряд сложных ошибок, одна из которых описывается ниже. Scope2 — дочерний объект области Scope1, а Scope1 предоставляет экземпляр A1 интерфейса A. Если кто-нибудь использует A1 из Scope2 (путем наследования) перед вызовом метода Scope2.provide() с помощью A2, то при последующем вызове метода Scope2.consume() может возвращаться не такой результат, как при предыдущем. Это может создавать сложности для разработчиков. |
|[`getParent()`](getparent-servicescope.md)     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | Возвращает родительскую область ServiceScope или неопределенное значение, если это корневая область. |
|[`provide(serviceKey,service)`](provide-servicescope.md)     | `public` | `T` | Метод ServiceScope.provide() позволяет зарегистрировать версию определенного объекта serviceKey для текущей области. Его можно использовать, только когда ServiceScope находится в "незавершенном" состоянии, т. е. до вызова метода finish(). |
|[`startNewChild()`](startnewchild-servicescope.md)     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | Создает дочернюю область ServiceScope. Для ключей, явно не предоставленных дочерней областью, используется родительская иерархия. |
|[`startNewRoot()`](startnewroot-servicescope.md)     | `public, static` | [`ServiceScope`](../sp-core-library/servicescope.md) | Создание новой корневой области ServiceScope. Только корневые области могут автоматически создавать версии объектов ServiceKey по умолчанию. |
|[`whenFinished(callback)`](whenfinished-servicescope.md)     | `public` | `void` | Если вызвать метод ServiceScope.consume() до вызова метода finish(), возникнет ошибка. Самый надежный способ защитить компонент от этой ошибки — вызывать метод consume() из функции обратного вызова whenFinished(). Если область службы уже готова, обратный вызов будет выполнен немедленно. В противном случае он будет выполнен позже, когда создание области будет завершено. |




