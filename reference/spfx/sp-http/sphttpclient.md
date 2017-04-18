# <a name="sphttpclient-class"></a>Класс SPHttpClient







SPHttpClient используется для выполнения вызовов REST для SharePoint. Он добавляет заголовки по умолчанию, управляет дайджестом, необходимым для записей, и собирает данные телеметрии, которые помогают службе отслеживать производительность приложения. Для связи со службами, не относящимися к SharePoint, используйте класс HttpClient.


## <a name="constructor"></a>constructor


**Подпись:** _constructor(serviceScope: [ServiceScope](../sp-core-library/servicescope.md));_

**Что возвращается**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`serviceKey`     | `public` | [`ServiceKey`](../sp-core-library/servicekey.md)<[`SPHttpClient`](../sp-http/sphttpclient.md)> | Ключ службы для SPHttpClient. |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`beginBatch()`](beginbatch-sphttpclient.md)     | `public` | `SPHttpClientBatch` | Начинает пакет ODATA, разрешающий собирать множество запросов REST в один веб-запрос. |
|[`fetch(url,configuration,options)`](fetch-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Как правило, параметры и семантика для SPHttpClient.fetch() фактически такие же, как в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org). Подкласс SPHttpClient добавляет некоторые дополнительные варианты поведения, удобные при работе с API ODATA SharePoint (этого можно избежать, используя в качестве альтернативы HttpClient). Вот эти варианты: добавляются заголовки "Accept" и "Content-Type" по умолчанию, если отсутствует явное указание; для операций записи автоматически добавляется заголовок "X-RequestDigest"; токен дайджеста запроса автоматически извлекается и хранится в кэше, при этом есть поддержка предварительной загрузки; для операций записи SPHttpClient автоматически добавляет заголовок "X-RequestDigest", который иногда нужно получать с помощью отдельного запроса, такого как "https://example.com/sites/sample/_api/contextinfo". Обычно можно подобрать соответствующий URL-адрес SPWeb путем поиска зарезервированного сегмента URL-адреса, например "_api", в исходном URL-адресе, переданном в fetch(). Если это не сработает, можно задать его явно с помощью ISPHttpClientOptions.webUrl. |
|[`get(url,configuration,options)`](get-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Вызывает fetch(), но задает метод GET. |
|[`getWebUrlFromRequestUrl(requestUrl)`](getweburlfromrequesturl-sphttpclient.md)     | `public, static` | `string` | При этом используется эвристика для подбора URL-адреса SPWeb, связанного с предоставленным URL-адресом REST. Это необходимо для таких операций, как пакетная обработка X-RequestDigest и ODATA, требующих отправки POST-запроса в отдельную конечную точку REST для выполнения запроса. Например, если для requestUrl задано "/sites/site/web/_api/service", возвращаемый URL-адрес будет "/sites/site/web". Если же для requestUrl задано "http://example.com/_layouts/service", возвращаемый URL-адрес будет "http://example.com". |
|[`post(url,configuration,options)`](post-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Вызывает fetch(), но задает метод POST. |





