# <a name="httpclientconfigurations-class"></a>Класс HttpClientConfigurations







Этот класс предоставляет стандартные предопределенные объекты HttpClientConfiguration для использования с классом HttpClient. Как правило, клиенты должны выбирать последний доступный номер версии, обеспечивающий использование всех параметров, рекомендованных для типичных сценариев. (Вместе с новыми параметрами будет введен новый номер версии, поэтому существующий код будет и дальше функционировать так же, как и во время тестирования.)



## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`none`     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | В этой конфигурации выключены все параметры функций для HttpClient. Поведение fetch() будет фактически таким же, как в API по стандарту WHATWG, описанному на сайте https://fetch.spec.whatwg.org. |
|`v1`     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Версия 1 обеспечивает использование таких параметров: consoleLogging=true |







