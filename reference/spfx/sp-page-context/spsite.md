# <a name="spsite-class"></a>Класс SPSite







Этот класс используется в основном с классом PageContext. Предоставляет контекстную информацию для семейства веб-сайтов SharePoint (сайта), в котором размещена страница.



## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`absoluteUrl`     | `public` | `string` | _Только для чтения._ Возвращает абсолютный URL-адрес SPSite. Пример: "https://example.com/sites/PubSite". |
|`cdnPrefix`     | `public` | `string` | _Только для чтения._ Возвращает указанный префикс сети CDN для приложения или нуль, если такого не существует. |
|`classification`     | `public` | `string` | _Только для чтения._ Возвращает классификацию сайта. |
|`correlationId`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Только для чтения._ Возвращает идентификатор корреляции для текущего запроса сервера. |
|`id`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Только для чтения._ GUID, определяющий SPSite на сервере. |
|`isNoScriptEnabled`     | `public` | `boolean` | _Только для чтения._ Возвращает значение true, если isNoScript включен для SPSite. |
|`recycleBinItemCount`     | `public` | `number` | _Только для чтения._ Количество элементов в корзине. |
|`serverRelativeUrl`     | `public` | `string` | _Только для чтения._ Возвращает связанный с сервером URL-адрес для SPSite. Пример: "/sites/PubSite". |
|`serverRequestPath`     | `public` | `string` | _Только для чтения._ Возвращает serverRelativeUrl исходного запроса. Пример: "/teams/SPClientTest/SitePages/Home.aspx". |
|`sitePagesEnabled`     | `public` | `boolean` | _Только для чтения._ Возвращает значение true, если SitePages включен для SPSite. |







