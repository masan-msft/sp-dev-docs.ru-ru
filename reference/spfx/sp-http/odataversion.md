# <a name="odataversion-class"></a>Класс ODataVersion







Представляет поддерживаемую версию заголовка "OData-Version", входящего в стандарт Open Data Protocol.



## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`v3`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | Представляет версию 3.0 для заголовка "OData-Version". |
|`v4`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | Представляет версию 4.0 для заголовка "OData-Version". |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`toString()`](tostring-odataversion.md)     | `public` | `string` | Возвращает значение "OData-Version", например "4.0". |
|[`tryParseFromHeaders()`](tryparsefromheaders-odataversion.md)     | `public, static` | [`ODataVersion`](../sp-http/odataversion.md) | При наличии заголовка "OData-Version" возвращает соответствующую константу ODataVersion. Если номер версии не поддерживается, возникает ошибка. Если заголовок отсутствует, возвращается значение "undefined". |





