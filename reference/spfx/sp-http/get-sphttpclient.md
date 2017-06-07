# <a name="geturlconfigurationoptions"></a>get(url,configuration,options)




Вызывает fetch(), но задает метод GET.

**Подпись:** _@override public get(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options?: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_

**Что возвращается**: `Promise<SPHttpClientResponse>`



Обещание, возвращающее результат.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес для получения. |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Определяет поведение по умолчанию SPHttpClient. Как правило, это должен быть номер последней версии из SPHttpClientConfigurations. |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | __Дополнительно.__ Дополнительные параметры, влияющие на запрос. |


