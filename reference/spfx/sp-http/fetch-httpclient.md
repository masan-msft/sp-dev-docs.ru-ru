<span data-ttu-id="69f57-p102">Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org).</span><span class="sxs-lookup"><span data-stu-id="69f57-p102">Performs a REST service call. Although the SPHttpClient subclass adds additional enhancements, the parameters and semantics for HttpClient.fetch() are essentially the same as the WHATWG API standard that is documented here: https://fetch.spec.whatwg.org/</span></span>

Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org).

<span data-ttu-id="69f57-106">**Подпись:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="69f57-106">**Signature:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span></span>

<span data-ttu-id="69f57-107">**Что возвращается**: `Promise<HttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="69f57-107">**Returns**: `Promise<HttpClientResponse>`</span></span>



<span data-ttu-id="69f57-108">Обещание, возвращающее результат.</span><span class="sxs-lookup"><span data-stu-id="69f57-108">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="69f57-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="69f57-109">Parameters</span></span>


| <span data-ttu-id="69f57-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="69f57-110">Parameter</span></span>    | <span data-ttu-id="69f57-111">Тип</span><span class="sxs-lookup"><span data-stu-id="69f57-111">Type</span></span>    | <span data-ttu-id="69f57-112">Описание</span><span class="sxs-lookup"><span data-stu-id="69f57-112">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="69f57-113">URL-адрес для получения.</span><span class="sxs-lookup"><span data-stu-id="69f57-113">the URL to fetch</span></span> |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | <span data-ttu-id="69f57-114">Определяет поведение по умолчанию HttpClient. Как правило, это должен быть номер последней версии из HttpClientConfigurations.</span><span class="sxs-lookup"><span data-stu-id="69f57-114">determines the default behavior of HttpClient; normally this should be the latest version number from HttpClientConfigurations</span></span> |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | <span data-ttu-id="69f57-115">Дополнительные параметры, влияющие на запрос.</span><span class="sxs-lookup"><span data-stu-id="69f57-115">additional options that affect the request</span></span> |


