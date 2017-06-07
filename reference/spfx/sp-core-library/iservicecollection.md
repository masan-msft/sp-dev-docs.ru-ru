# <a name="iservicecollection-interface"></a>Интерфейс IServiceCollection







Сокращенный шаблон для извлечения известных служб из объекта ServiceScope.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`serviceScope`      | [`ServiceScope`](../sp-core-library/servicescope.md) | Возвращает базовый объект ServiceScope, к которому относятся элементы. |






### <a name="remarks"></a>Заметки

Многоразовые компоненты библиотеки обычно объявляют свои зависимости служб, вызывая метод ServiceScope.consume() с помощью соответствующего объекта ServiceKey для каждой службы. Для бизнес-логики приложений или небольших проектов такой формализм может быть излишним и увеличивать время, которое требуется на обучение разработчиков. Шаблон IServiceCollection позволяет передавать общие службы для определенного сценария в виде простой, удобной коллекции. Например, функция виджета может добавлять следующий интерфейс: interface IWidgetServiceCollection extends IServiceCollection { spHttpClient: SPHttpClient; widgetManager: IWidgetManager; } После этого класс Widget может инициализировать свойство services следующим образом: class Widget { private _services: IWidgetServiceCollection; constructor(serviceScope: ServiceScope) { serviceScope.whenFinished(() => { this._services = { serviceScope, spHttpClient: serviceScope.consume(SPHttpClient.serviceKey), widgetManager: serviceScope.consume(WidgetManager.ServiceKey), }; }); } public get services(): IWidgetServiceCollection { return this._services; } } Для группы компонентов, обладающих этими зависимостями, такой объект services можно передавать вместо абстрактного объекта ServiceScope. Это позволяет использовать прямые ссылки, например services.widgetManager, services.spHttpClient и т. д. Для нетипичных зависимостей можно использовать класс services.serviceScope. ВАЖНО! Чтобы шаблон был удобным и понятным, НЕ следует добавлять в интерфейс IServiceCollection элементы, не являющиеся службами ServiceScope.

