# <a name="converttoodatastringliteral"></a>convertToODataStringLiteral()




Преобразует переменную в строковый литерал OData, подходящий для использования в URL-адресе REST. Возвращаемая строка заключается в одиночные кавычки, а все одиночные кавычки экранируются. Пример использования: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"

**Подпись:** _public static convertToODataStringLiteral(value: string): string;_

**Возвращаемое значение**: `string`





#### <a name="parameters"></a>Параметры
Нет


