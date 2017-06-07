# <a name="sphttpclientcommonconfiguration-class"></a>Класс SPHttpClientCommonConfiguration

_Реализация: [`ISPHttpClientCommonConfiguration`](../sp-http/isphttpclientcommonconfiguration.md)_





Общий базовый класс для SPHttpClientConfiguration и SPHttpClientBatchConfiguration.


## <a name="constructor"></a>constructor
Создает экземпляр SPHttpClientCommonConfiguration с помощью указанных флажков. Значения по умолчанию будут использоваться для любых отсутствующих или неопределенных флажков. Если указан overrideFlags, он переопределяет флажки.

**Подписи:** _constructor(flags: [ISPHttpClientCommonConfiguration](../sp-http/isphttpclientcommonconfiguration.md), overrideFlags?: ISPHttpClientCommonConfiguration);_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`flags`     | `public` | [`ISPHttpClientCommonConfiguration`](../sp-http/isphttpclientcommonconfiguration.md) |  |
|`jsonRequest`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.jsonRequest} |
|`jsonResponse`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.jsonResponse} |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-sphttpclientcommonconfiguration.md)     | `protected` | `void` |  |
|[`overrideWith()`](overridewith-sphttpclientcommonconfiguration.md)     | `public` | [`SPHttpClientCommonConfiguration`](../sp-http/sphttpclientcommonconfiguration.md) |  |





