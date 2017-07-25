<span data-ttu-id="09b41-p101">При наличии заголовка "OData-Version" возвращает соответствующую константу ODataVersion. Если номер версии не поддерживается, возникает ошибка. Если заголовок отсутствует, возвращается значение "undefined".</span><span class="sxs-lookup"><span data-stu-id="09b41-p101">If the 'OData-Version' header is present, this returns the corresponding ODataVersion constant. An error is thrown if the version number is not supported. If the header is missing, then undefined is returned.</span></span>




При наличии заголовка "OData-Version" возвращает соответствующую константу ODataVersion. Если номер версии не поддерживается, возникает ошибка. Если заголовок отсутствует, возвращается значение "undefined".

<span data-ttu-id="09b41-105">**Подпись:** _public static tryParseFromHeaders(headers: Headers): [ODataVersion](../sp-http/odataversion.md);_</span><span class="sxs-lookup"><span data-stu-id="09b41-105">**Signature:** _public static tryParseFromHeaders(headers: Headers): [ODataVersion](../sp-http/odataversion.md);_</span></span>

<span data-ttu-id="09b41-106">**Что возвращается**: [`ODataVersion`](../sp-http/odataversion.md)</span><span class="sxs-lookup"><span data-stu-id="09b41-106">**Returns**: [`ODataVersion`](../sp-http/odataversion.md)</span></span>





#### <a name="parameters"></a><span data-ttu-id="09b41-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="09b41-107">Parameters</span></span>
<span data-ttu-id="09b41-108">Нет</span><span class="sxs-lookup"><span data-stu-id="09b41-108">None</span></span>


