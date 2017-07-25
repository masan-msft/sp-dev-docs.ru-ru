<span data-ttu-id="0a437-p101">Удаляет косую черту в конце URL-адреса. Эта функция предполагает, что входная строка уже является действительным URL-адресом (абсолютным или относительным). Примеры: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> ''</span><span class="sxs-lookup"><span data-stu-id="0a437-p101">Removes any slash characters from the end of the URL. This function assumes that the input is already a valid absolute or server-relative URL. Examples: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> ''</span></span>




Удаляет косую черту в конце URL-адреса. Эта функция предполагает, что входная строка уже является действительным URL-адресом (абсолютным или относительным). Примеры: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> ''

<span data-ttu-id="0a437-105">**Подпись:** _public static removeEndSlash(url: string): string;_</span><span class="sxs-lookup"><span data-stu-id="0a437-105">**Signature:** _public static removeEndSlash(url: string): string;_</span></span>

<span data-ttu-id="0a437-106">**Возвращаемое значение**: `string`</span><span class="sxs-lookup"><span data-stu-id="0a437-106">**Returns**: `string`</span></span>





#### <a name="parameters"></a><span data-ttu-id="0a437-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="0a437-107">Parameters</span></span>


| <span data-ttu-id="0a437-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="0a437-108">Parameter</span></span>    | <span data-ttu-id="0a437-109">Тип</span><span class="sxs-lookup"><span data-stu-id="0a437-109">Type</span></span>    | <span data-ttu-id="0a437-110">Описание</span><span class="sxs-lookup"><span data-stu-id="0a437-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="0a437-111">Нормализуемый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="0a437-111">the URL to be normalized</span></span> |


