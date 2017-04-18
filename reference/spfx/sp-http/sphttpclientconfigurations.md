# <a name="sphttpclientconfigurations-class"></a>Класс SPHttpClientConfigurations







Этот класс предоставляет стандартные предопределенные объекты SPHttpClientConfiguration для использования с классом SPHttpClient. Как правило, клиенты должны выбирать последний доступный номер версии, обеспечивающий использование всех параметров, рекомендованных для типичных сценариев. (Вместе с новыми параметрами будет введен новый номер версии, поэтому существующий код будет и дальше функционировать так же, как и во время тестирования.)



## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`none`     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | В этой конфигурации выключены все параметры функций для HttpClient. Поведение fetch() будет фактически таким же, как в API по стандарту WHATWG, описанному на сайте https://fetch.spec.whatwg.org. |
|`v1`     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Версия 1 обеспечивает использование следующих параметров: consoleLogging = true; jsonRequest = true; jsonResponse = true; defaultSameOriginCredentials = true; defaultODataVersion = ODataVersion.v4; requestDigest = true. |







