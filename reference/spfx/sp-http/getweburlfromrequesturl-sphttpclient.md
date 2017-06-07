# <a name="getweburlfromrequesturlrequesturl"></a>getWebUrlFromRequestUrl(requestUrl)




При этом используется эвристика для подбора URL-адреса SPWeb, связанного с предоставленным URL-адресом REST. Это необходимо для таких операций, как пакетная обработка X-RequestDigest и ODATA, требующих отправки POST-запроса в отдельную конечную точку REST для выполнения запроса. Например, если для requestUrl задано "/sites/site/web/_api/service", возвращаемый URL-адрес будет "/sites/site/web". Если же для requestUrl задано "http://example.com/_layouts/service", возвращаемый URL-адрес будет "http://example.com".

**Подпись:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_

**Что возвращается**: `string`



Выводимый URL-адрес SPWeb.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `requestUrl`    | `string` | URL-адрес для службы REST SharePoint. |


