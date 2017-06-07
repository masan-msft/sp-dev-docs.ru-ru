# <a name="httpclient-class"></a>Класс HttpClient







HttpClient внедряет базовый набор функций для выполнения операций REST. Подкласс SPHttpClient расширяет базовые функции с помощью расширений для SharePoint.


## <a name="constructor"></a>constructor


**Подпись:** _constructor(serviceScope: [ServiceScope](../sp-core-library/servicescope.md));_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`serviceKey`     | `public` | [`ServiceKey`](../sp-core-library/servicekey.md)<[`HttpClient`](../sp-http/httpclient.md)> | Ключ службы для HttpClient. Примечание. Это будет доступно в **бета-режиме**. Не рекомендуем для использования в среде производства. |
|`serviceScope`     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | _Только для чтения._ ServiceScope, который передается в constructor. |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`fetch(url,configuration,options)`](fetch-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org). |
|[`fetchCore()`](fetchcore-httpclient.md)     | `protected` | `Promise<Response>` | Все сетевые запросы маршрутизируются с помощью этого метода, вызывающего IFetchProvider.fetch(). |
|[`get(url,configuration,options)`](get-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Вызывает fetch(), но задает метод GET. |
|[`post(url,configuration,options)`](post-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Вызывает fetch(), но задает метод POST. |





