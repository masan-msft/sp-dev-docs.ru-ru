# <a name="httpclientconfiguration-class"></a>Класс HttpClientConfiguration

_Реализация: [`IHttpClientConfiguration`](../sp-http/ihttpclientconfiguration.md)_



Используется в бета-режиме.

Объект HttpClientConfiguration предоставляет набор параметров для включения или выключения различных возможностей класса HttpClient. Обычно эти параметры задаются (например, при вызове HttpClient.fetch()) путем предоставления одного из предопределенных значений по умолчанию из HttpClientConfigurations, но эти параметры можно также изменять с помощью метода HttpClientConfiguration.overrideWith().


## <a name="constructor"></a>constructor
Создает новый экземпляр HttpClientConfiguration с использованием указанных флажков. Значения по умолчанию будут использоваться для любых отсутствующих или неопределенных флажков. Если указан параметр overrideFlags, он переопределяет флажки.*

**Подписи:** _constructor(flags: [IHttpClientConfiguration](../sp-http/ihttpclientconfiguration.md), overrideFlags?: IHttpClientConfiguration);_

**Что возвращается**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`consoleLogging`     | `public` | `boolean` | _Только для чтения._ {@inheritdoc IHttpClientConfiguration.consoleLogging} |
|`flags`     | `public` | [`IHttpClientConfiguration`](../sp-http/ihttpclientconfiguration.md) |  |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-httpclientconfiguration.md)     | `protected` | `void` | Дочерние классы должны переопределять этот метод для инициализации объекта флажков. |
|[`overrideWith()`](overridewith-httpclientconfiguration.md)     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Дочерние классы должны переопределять этот метод для создания типа дочернего класса, а не типа базового класса. |





