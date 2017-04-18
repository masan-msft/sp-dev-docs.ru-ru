# <a name="iwebpartcontext-interface"></a>Интерфейс IWebPartContext







Интерфейс базового контекста для клиентских веб-частей.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`domElement`      | `HTMLElement` | Ссылка на элемент DOM, в котором размещен этот клиентский компонент. |
|`httpClient`      | [`HttpClient`](../sp-http/httpclient.md) | Экземпляр HttpClient, связанный с этой веб-частью. |
|`instanceId`      | `string` | Идентификатор экземпляра веб-части. Это глобальное уникальное значение. |
|`manifest`      | `IClientSideWebPartManifestInstance<any>` | Манифест для клиентской веб-части. |
|`pageContext`      | [`PageContext`](../sp-page-context/pagecontext.md) | Контекст страницы SharePoint. |
|`propertyPane`      | `IPropertyPaneAccessor` | Метод доступа к распространенным операциям области свойств веб части. |
|`spHttpClient`      | [`SPHttpClient`](../sp-http/sphttpclient.md) | Экземпляр SPHttpClient, связанный с этой веб-частью. |
|`statusRenderer`      | [`IClientSideWebPartStatusRenderer`](../sp-webpart-base/iclientsidewebpartstatusrenderer.md) | Отрисовщик состояния веб-части. |
|`webPartTag`      | `string` | Тег веб-части, используемый для ведения журнала и телеметрии. |






### <a name="remarks"></a>Примечания

Объект "context" — это набор известных служб и других объектов, которые, скорее всего, понадобятся бизнес-логике, работающей с компонентом. У каждого типа компонента есть собственное расширение для этого интерфейса, например IWebPartContext для веб-частей ICodePartContext для частей кода и т. д.

