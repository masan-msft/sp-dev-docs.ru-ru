<span data-ttu-id="1d7d3-p101">При этом используется эвристика для подбора URL-адреса SPWeb, связанного с предоставленным URL-адресом REST. Это необходимо для таких операций, как пакетная обработка X-RequestDigest и ODATA, требующих отправки POST-запроса в отдельную конечную точку REST для выполнения запроса. Например, если для requestUrl задано "/sites/site/web/_api/service", возвращаемый URL-адрес будет "/sites/site/web". Если же для requestUrl задано "http://example.com/_layouts/service", возвращаемый URL-адрес будет "http://example.com".</span><span class="sxs-lookup"><span data-stu-id="1d7d3-p101">This uses a heuristic to guess the SPWeb URL associated with the provided REST URL. This is necessary for operations such as the X-RequestDigest and ODATA batching, which require POSTing to a separate REST endpoint in order to complete a request. For excample, if the requestUrl is "/sites/site/web/_api/service", the returned URL would be "/sites/site/web". Or if the requestUrl is "http://example.com/_layouts/service", the returned URL would be "http://example.com".</span></span>




При этом используется эвристика для подбора URL-адреса SPWeb, связанного с предоставленным URL-адресом REST. Это необходимо для таких операций, как пакетная обработка X-RequestDigest и ODATA, требующих отправки POST-запроса в отдельную конечную точку REST для выполнения запроса. Например, если для requestUrl задано "/sites/site/web/_api/service", возвращаемый URL-адрес будет "/sites/site/web". Если же для requestUrl задано "http://example.com/_layouts/service", возвращаемый URL-адрес будет "http://example.com".

<span data-ttu-id="1d7d3-106">**Подпись:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_</span><span class="sxs-lookup"><span data-stu-id="1d7d3-106">**Signature:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_</span></span>

<span data-ttu-id="1d7d3-107">**Что возвращается**: `string`</span><span class="sxs-lookup"><span data-stu-id="1d7d3-107">**Returns**: `string`</span></span>



<span data-ttu-id="1d7d3-108">Выводимый URL-адрес SPWeb.</span><span class="sxs-lookup"><span data-stu-id="1d7d3-108">the inferred SPWeb URL</span></span>

#### <a name="parameters"></a><span data-ttu-id="1d7d3-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="1d7d3-109">Parameters</span></span>


| <span data-ttu-id="1d7d3-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="1d7d3-110">Parameter</span></span>    | <span data-ttu-id="1d7d3-111">Тип</span><span class="sxs-lookup"><span data-stu-id="1d7d3-111">Type</span></span>    | <span data-ttu-id="1d7d3-112">Описание</span><span class="sxs-lookup"><span data-stu-id="1d7d3-112">Description</span></span> |
|:-------------|:---------------|:------------|
| `requestUrl`    | `string` | <span data-ttu-id="1d7d3-113">URL-адрес для службы REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1d7d3-113">The URL for a SharePoint REST service</span></span> |


