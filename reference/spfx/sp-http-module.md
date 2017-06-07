# <a name="sp-http-module"></a>Модуль sp-http



## <a name="classes"></a>Классы

| Класс    |  Описание |
|:-------------|:---------------|
| [`HttpClient`](./sp-http/httpclient.md)     | В классе HttpClient реализован базовый набор функций для выполнения операций REST. Подкласс SPHttpClient расширяет этот базовый набор функций с помощью специальных расширений для SharePoint. |
| [`HttpClientConfiguration`](./sp-http/httpclientconfiguration.md)     | Объект HttpClientConfiguration предоставляет набор параметров для включения или выключения различных возможностей класса HttpClient. Обычно эти параметры задаются (например, при вызове HttpClient.fetch()) путем предоставления одного из предопределенных значений по умолчанию из HttpClientConfigurations, но эти параметры можно также изменять с помощью метода HttpClientConfiguration.overrideWith(). |
| [`HttpClientConfigurations`](./sp-http/httpclientconfigurations.md)     | Этот класс предоставляет стандартные предопределенные объекты HttpClientConfiguration для использования с классом HttpClient. Как правило, клиенты должны выбирать последний доступный номер версии, позволяющий использовать все параметры, рекомендованные для типичных сценариев. (Вместе с новыми параметрами будет введен новый номер версии, поэтому имеющийся код продолжит работать таким же образом, как и во время тестирования.) |
| [`HttpClientResponse`](./sp-http/httpclientresponse.md)     | Подкласс Response, возвращаемый такими методами, как HttpClient.fetch(). |
| [`ODataVersion`](./sp-http/odataversion.md)     | Представляет поддерживаемую версию заголовка OData-Version, входящего в стандарт Open Data Protocol. |
| [`SPHttpClient`](./sp-http/sphttpclient.md)     | Класс SPHttpClient используется для выполнения вызовов REST к SharePoint. Он добавляет заголовки по умолчанию, управляет дайджестом, необходимым для записи, и собирает данные телеметрии, которые помогают службе отслеживать производительность приложения. Для связи со службами, не относящимися к SharePoint, используйте класс HttpClient. |
| [`SPHttpClientCommonConfiguration`](./sp-http/sphttpclientcommonconfiguration.md)     | Общий базовый класс для SPHttpClientConfiguration и SPHttpClientBatchConfiguration. |
| [`SPHttpClientConfiguration`](./sp-http/sphttpclientconfiguration.md)     | Объект SPHttpClientConfiguration предоставляет набор переключателей для включения и выключения различных функций класса SPHttpClient. Как правило, значения этих параметров задаются, например при вызове метода SPHttpClient.fetch(), путем предоставления одного из предопределенных значений по умолчанию из объекта SPHttpClientConfigurations, но их также можно изменять с помощью метода SPHttpClientConfiguration.overrideWith(). |
| [`SPHttpClientConfigurations`](./sp-http/sphttpclientconfigurations.md)     | Этот класс предоставляет стандартные предопределенные объекты SPHttpClientConfiguration для использования с классом SPHttpClient. Как правило, клиенты должны выбирать последний доступный номер версии, позволяющий использовать все параметры, рекомендованные для типичных сценариев. (Вместе с новыми параметрами будет введен новый номер версии, поэтому имеющийся код продолжит работать таким же образом, как и во время тестирования.) |
| [`SPHttpClientResponse`](./sp-http/sphttpclientresponse.md)     | Подкласс Response, возвращаемый такими методами, как SPHttpClient.fetch(). |



## <a name="interfaces"></a>Интерфейсы

| Интерфейс    |  Описание |
|:-------------|:---------------|
| [`IHttpClientConfiguration`](./sp-http/ihttpclientconfiguration.md)   | Интерфейс флажков для HttpClientConfiguration.  |
| [`IHttpClientOptions`](./sp-http/ihttpclientoptions.md)   | В этом интерфейсе определены параметры для таких операций HttpClient, как get(), post(), fetch(). Он основан на параметрах стандарта WHATWG для API, приведенных на сайте https://fetch.spec.whatwg.org.  |
| [`ISPHttpClientCommonConfiguration`](./sp-http/isphttpclientcommonconfiguration.md)   | Интерфейс флажков для SPHttpClientCommonConfiguration  |
| [`ISPHttpClientConfiguration`](./sp-http/isphttpclientconfiguration.md)   | Интерфейс флажков для SPHttpClientConfiguration.  |
| [`ISPHttpClientOptions`](./sp-http/isphttpclientoptions.md)   | В этом интерфейсе определены параметры для таких операций класса SPHttpClient, как get(), post(), fetch() и т. д. Он основан на стандартных параметрах API WHATWG, описанных здесь: https://fetch.spec.whatwg.org/  |






