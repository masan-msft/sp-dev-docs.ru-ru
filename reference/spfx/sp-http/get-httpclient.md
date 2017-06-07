# <a name="geturlconfigurationoptions"></a>get(url,configuration,options)




Вызывает fetch(), но задает метод GET.

**Подпись:** _@virtual public get(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options?: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_

**Что возвращается**: `Promise<HttpClientResponse>`



Обещание, возвращающее результат.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес для получения. |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Определяет поведение по умолчанию HttpClient. Как правило, это должен быть номер последней версии из HttpClientConfigurations. |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | _Дополнительно._ Дополнительные параметры, влияющие на запрос. |
