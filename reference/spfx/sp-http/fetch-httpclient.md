# <a name="fetchurlconfigurationoptions"></a>fetch(url,configuration,options)


 Примечание. Это будет доступно в **бета-режиме**. Не рекомендуем использовать этот метод в рабочей среде.

Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org).

**Подпись:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_

**Что возвращается**: `Promise<HttpClientResponse>`



Обещание, возвращающее результат.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес для получения. |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Определяет поведение по умолчанию HttpClient. Как правило, это должен быть номер последней версии из HttpClientConfigurations. |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | Дополнительные параметры, влияющие на запрос. |


