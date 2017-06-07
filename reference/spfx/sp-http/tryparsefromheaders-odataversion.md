# <a name="tryparsefromheaders"></a>tryParseFromHeaders()




При наличии заголовка "OData-Version" возвращает соответствующую константу ODataVersion. Если номер версии не поддерживается, возникает ошибка. Если заголовок отсутствует, возвращается значение "undefined".

**Подпись:** _public static tryParseFromHeaders(headers: Headers): [ODataVersion](../sp-http/odataversion.md);_

**Что возвращается**: [`ODataVersion`](../sp-http/odataversion.md)





#### <a name="parameters"></a>Параметры
Нет


