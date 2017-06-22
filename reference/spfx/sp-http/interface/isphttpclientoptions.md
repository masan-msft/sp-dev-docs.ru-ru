# <a name="isphttpclientoptions-interface"></a>Интерфейс ISPHttpClientOptions







В этом интерфейсе определены параметры для таких операций SPHttpClient, как get(), post(), fetch(). Он основан на параметрах стандарта WHATWG для API, приведенных на сайте https://fetch.spec.whatwg.org.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`webUrl`      | `string` | Для операции записи SPHttpClient автоматически добавит заголовок "X-RequestDigest", который иногда нужно получать с помощью отдельного запроса, например "https://example.com/sites/sample/_api/contextinfo". Обычно URL-адрес SPWeb (в данном примере "https://example.com/sites/sample") можно определить, посмотрев на такой зарезервированный сегмент URL-адреса, как "_api", в исходном запросе REST, но определенные конечные точки REST не содержат зарезервированного сегмента URL-адреса. В данном случае webUrl можно явно указать с помощью этого параметра. |






