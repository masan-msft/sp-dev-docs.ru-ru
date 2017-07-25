<span data-ttu-id="2ed5b-p101">Преобразует переменную в строковый литерал OData, подходящий для использования в URL-адресе REST. Возвращаемая строка заключается в одиночные кавычки, а все одиночные кавычки экранируются. Пример использования: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"</span><span class="sxs-lookup"><span data-stu-id="2ed5b-p101">Converts a variable to an OData string literal suitable for usage in a REST URL. The returned string will be enclosed in single quotes, and any single quotes will be escaped. Example usage: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"</span></span>




Преобразует переменную в строковый литерал OData, подходящий для использования в URL-адресе REST. Возвращаемая строка заключается в одиночные кавычки, а все одиночные кавычки экранируются. Пример использования: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"

<span data-ttu-id="2ed5b-105">**Подпись:** _public static convertToODataStringLiteral(value: string): string;_</span><span class="sxs-lookup"><span data-stu-id="2ed5b-105">**Signature:** _public static convertToODataStringLiteral(value: string): string;_</span></span>

<span data-ttu-id="2ed5b-106">**Возвращаемое значение**: `string`</span><span class="sxs-lookup"><span data-stu-id="2ed5b-106">**Returns**: `string`</span></span>





#### <a name="parameters"></a><span data-ttu-id="2ed5b-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="2ed5b-107">Parameters</span></span>
<span data-ttu-id="2ed5b-108">Нет</span><span class="sxs-lookup"><span data-stu-id="2ed5b-108">None</span></span>


