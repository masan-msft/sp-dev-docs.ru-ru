# <a name="urlutilities-class"></a>Класс UrlUtilities







Распространенные вспомогательные функции для работы с URL-адресами. Эти служебные программы отличаются простотой, небольшим размером и широкими возможностями применения.






## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Возвращаемое значение  | Описание|
|:-------------|:----|:-------|:-----------|
|[`convertToODataStringLiteral()`](converttoodatastringliteral-urlutilities.md)     | `public, static` | `string` | Преобразует переменную в строковый литерал OData, подходящий для использования в URL-адресе REST. Возвращаемая строка заключается в одиночные кавычки, а все одиночные кавычки экранируются. Пример использования: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files" |
|[`removeEndSlash(url)`](removeendslash-urlutilities.md)     | `public, static` | `string` | Удаляет косую черту в конце URL-адреса. Эта функция предполагает, что входная строка уже является действительным URL-адресом (абсолютным или относительным). Примеры: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> '' |





