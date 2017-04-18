# <a name="posturlconfigurationoptions"></a>post(url,configuration,options)




Вызывает fetch(), но задает метод POST.

**Подпись:** _@override public post(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_

**Что возвращается**: `Promise<SPHttpClientResponse>`



Обещание, возвращающее результат.

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес для получения. |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Определяет поведение по умолчанию SPHttpClient. Как правило, это должен быть номер последней версии из SPHttpClientConfigurations. |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | Дополнительные параметры, влияющие на запрос. |


