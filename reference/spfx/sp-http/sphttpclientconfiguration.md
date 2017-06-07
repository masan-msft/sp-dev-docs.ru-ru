# <a name="sphttpclientconfiguration-class"></a>Класс SPHttpClientConfiguration

_Реализация: [`ISPHttpClientConfiguration`](../sp-http/isphttpclientconfiguration.md)_





Объект SPHttpClientConfiguration предоставляет набор параметров для включения или выключения различных возможностей класса SPHttpClient. Обычно эти параметры задаются (например, при вызове SPHttpClient.fetch()) путем предоставления одного из предопределенных значений по умолчанию из SPHttpClientConfigurations, но эти параметры можно также изменять с помощью метода SPHttpClientConfiguration.overrideWith().


## <a name="constructor"></a>constructor
Создает новый экземпляр SPHttpClientConfiguration с помощью указанных флажков. Значения по умолчанию будут использоваться для любых отсутствующих или неопределенных флажков. Если указан overrideFlags, он переопределяет флажки.

**Подписи:** _constructor(flags: [ISPHttpClientConfiguration](../sp-http/isphttpclientconfiguration.md), overrideFlags?: ISPHttpClientConfiguration);_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`defaultODataVersion`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.defaultODataVersion} |
|`defaultSameOriginCredentials`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.defaultSameOriginCredentials} |
|`flags`     | `public` | [`ISPHttpClientConfiguration`](../sp-http/isphttpclientconfiguration.md) |  |
|`requestDigest`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.requestDigest} |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-sphttpclientconfiguration.md)     | `protected` | `void` |  |
|[`overrideWith()`](overridewith-sphttpclientconfiguration.md)     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) |  |





