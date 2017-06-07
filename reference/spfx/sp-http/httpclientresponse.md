# <a name="httpclientresponse-class"></a>Класс HttpClientResponse

_Реализация: `Response`_





Подкласс Response, возвращаемый такими методами, как HttpClient.fetch().



## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`bodyUsed`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc Body.bodyUsed} |
|`headers`     | `public` | `Headers` | _Только для чтения._ {@inheritdoc Response.headers} |
|`nativeResponse`     | `public` | `Response` |  |
|`ok`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc Response.ok} |
|`status`     | `public` | `number` | _Только для чтения._ {@inheritdoc Response.status} |
|`statusText`     | `public` | `string` | _Только для чтения._ {@inheritdoc Response.statusText} |
|`type`     | `public` | `ResponseType` | _Только для чтения._ {@inheritdoc Response.type} |
|`url`     | `public` | `string` | _Только для чтения._ {@inheritdoc Response.url} |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`arrayBuffer()`](arraybuffer-httpclientresponse.md)     | `public` | `Promise<ArrayBuffer>` | {@inheritdoc Body.arrayBuffer} |
|[`blob()`](blob-httpclientresponse.md)     | `public` | `Promise<Blob>` | {@inheritdoc Body.blob} |
|[`clone()`](clone-httpclientresponse.md)     | `public` | [`HttpClientResponse`](../sp-http/httpclientresponse.md) |  |
|[`error()`](error-httpclientresponse.md)     | `public, static` | `Response` | {@inheritdoc Response.error} |
|[`formData()`](formdata-httpclientresponse.md)     | `public` | `Promise<FormData>` | {@inheritdoc Body.formData} |
|[`json()`](json-httpclientresponse.md)     | `public` | `Promise<any>` | {@inheritdoc Body.json} |
|[`redirect()`](redirect-httpclientresponse.md)     | `public, static` | `Response` | {@inheritdoc Response.redirect} |
|[`text()`](text-httpclientresponse.md)     | `public` | `Promise<string>` | {@inheritdoc Body.text} |





### <a name="remarks"></a>Заметки

Это заполнитель. В будущем к этому классу может быть добавлена специальная функциональность для HttpClient.

