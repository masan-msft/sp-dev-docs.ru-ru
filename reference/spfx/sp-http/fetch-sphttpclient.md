# <a name="fetchurlconfigurationoptions"></a>fetch(url,configuration,options)




Как правило, параметры и семантика для SPHttpClient.fetch() фактически такие же, как в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org). Подкласс SPHttpClient добавляет некоторые дополнительные варианты поведения, удобные при работе с API ODATA SharePoint (этого можно избежать, используя в качестве альтернативы HttpClient). Вот эти варианты: добавляются заголовки "Accept" и "Content-Type" по умолчанию, если отсутствует явное указание; для операций записи автоматически добавляется заголовок "X-RequestDigest"; токен дайджеста запроса автоматически извлекается и хранится в кэше, при этом есть поддержка предварительной загрузки; для операций записи SPHttpClient автоматически добавляет заголовок "X-RequestDigest", который иногда нужно получать с помощью отдельного запроса, такого как "https://example.com/sites/sample/_api/contextinfo". Обычно можно подобрать соответствующий URL-адрес SPWeb путем поиска зарезервированного сегмента URL-адреса, например "_api", в исходном URL-адресе, переданном в fetch(). Если это не сработает, можно задать его явно с помощью ISPHttpClientOptions.webUrl.

**Подпись:** _@override public fetch(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_

**Что возвращается**: `Promise<SPHttpClientResponse>`



Обещание, возвращающее результат.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес для получения. |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Определяет поведение по умолчанию SPHttpClient. Как правило, это должен быть номер последней версии из SPHttpClientConfigurations. |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | Дополнительные параметры, влияющие на запрос. |


