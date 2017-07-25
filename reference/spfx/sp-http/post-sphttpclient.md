# <a name="posturlconfigurationoptions"></a><span data-ttu-id="cc40e-101">post(url,configuration,options)</span><span class="sxs-lookup"><span data-stu-id="cc40e-101">post(url,configuration,options)</span></span>




<span data-ttu-id="cc40e-102">Вызывает fetch(), но задает метод POST.</span><span class="sxs-lookup"><span data-stu-id="cc40e-102">Calls fetch(), but sets the method to 'POST'.</span></span>

<span data-ttu-id="cc40e-103">**Подпись:** _@override public post(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="cc40e-103">**Signature:** _@override public post(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_</span></span>

<span data-ttu-id="cc40e-104">**Что возвращается**: `Promise<SPHttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="cc40e-104">**Returns**: `Promise<SPHttpClientResponse>`</span></span>



<span data-ttu-id="cc40e-105">Обещание, возвращающее результат.</span><span class="sxs-lookup"><span data-stu-id="cc40e-105">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="cc40e-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc40e-106">Parameters</span></span>


| <span data-ttu-id="cc40e-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="cc40e-107">Parameter</span></span>    | <span data-ttu-id="cc40e-108">Тип</span><span class="sxs-lookup"><span data-stu-id="cc40e-108">Type</span></span>    | <span data-ttu-id="cc40e-109">Описание</span><span class="sxs-lookup"><span data-stu-id="cc40e-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="cc40e-110">URL-адрес для получения.</span><span class="sxs-lookup"><span data-stu-id="cc40e-110">the URL to fetch</span></span> |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | <span data-ttu-id="cc40e-111">Определяет поведение по умолчанию SPHttpClient. Как правило, это должен быть номер последней версии из SPHttpClientConfigurations.</span><span class="sxs-lookup"><span data-stu-id="cc40e-111">determines the default behavior of SPHttpClient; normally this should be the latest version number from SPHttpClientConfigurations</span></span> |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | <span data-ttu-id="cc40e-112">Дополнительные параметры, влияющие на запрос.</span><span class="sxs-lookup"><span data-stu-id="cc40e-112">additional options that affect the request</span></span> |


