# <a name="posturlconfigurationoptions"></a><span data-ttu-id="ed502-101">post(url,configuration,options)</span><span class="sxs-lookup"><span data-stu-id="ed502-101">post(url,configuration,options)</span></span>




<span data-ttu-id="ed502-102">Вызывает fetch(), но задает метод POST.</span><span class="sxs-lookup"><span data-stu-id="ed502-102">Calls fetch(), but sets the method to 'POST'.</span></span>

<span data-ttu-id="ed502-103">**Подпись:** _@virtual public post(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="ed502-103">**Signature:** _@virtual public post(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span></span>

<span data-ttu-id="ed502-104">**Что возвращается**: `Promise<HttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="ed502-104">**Returns**: `Promise<HttpClientResponse>`</span></span>



<span data-ttu-id="ed502-105">Обещание, возвращающее результат.</span><span class="sxs-lookup"><span data-stu-id="ed502-105">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="ed502-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="ed502-106">Parameters</span></span>


| <span data-ttu-id="ed502-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="ed502-107">Parameter</span></span>    | <span data-ttu-id="ed502-108">Тип</span><span class="sxs-lookup"><span data-stu-id="ed502-108">Type</span></span>    | <span data-ttu-id="ed502-109">Описание</span><span class="sxs-lookup"><span data-stu-id="ed502-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="ed502-110">URL-адрес для получения.</span><span class="sxs-lookup"><span data-stu-id="ed502-110">the URL to fetch</span></span> |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | <span data-ttu-id="ed502-111">Определяет поведение по умолчанию HttpClient. Как правило, это должен быть номер последней версии из HttpClientConfigurations.</span><span class="sxs-lookup"><span data-stu-id="ed502-111">determines the default behavior of HttpClient; normally this should be the latest version number from HttpClientConfigurations</span></span> |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | <span data-ttu-id="ed502-112">Дополнительные параметры, влияющие на запрос.</span><span class="sxs-lookup"><span data-stu-id="ed502-112">additional options that affect the request</span></span> |


