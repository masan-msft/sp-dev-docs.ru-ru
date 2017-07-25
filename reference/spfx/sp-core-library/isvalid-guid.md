<span data-ttu-id="6c1bc-p101">Указывает, является ли GUID допустимым, т. е. можно ли его анализировать с помощью метода Guid.tryParse(). Эта функция работает быстрее, чем Guid.tryParse(), так как она не создает объект Guid.</span><span class="sxs-lookup"><span data-stu-id="6c1bc-p101">Indicates whether a guid is valid, i.e. whether it would be successfully parsed by Guid.tryParse(). This function is cheaper than Guid.tryParse() because it does not construct a Guid object.</span></span>




Указывает, является ли GUID допустимым, т. е. можно ли его анализировать с помощью метода Guid.tryParse(). Эта функция работает быстрее, чем Guid.tryParse(), так как она не создает объект Guid.

<span data-ttu-id="6c1bc-104">**Подпись:** _public static isValid(guid: string): boolean;_</span><span class="sxs-lookup"><span data-stu-id="6c1bc-104">**Signature:** _public static isValid(guid: string): boolean;_</span></span>

<span data-ttu-id="6c1bc-105">**Возвращаемое значение**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="6c1bc-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="6c1bc-106">Значение true, если объект Guid является допустимым.</span><span class="sxs-lookup"><span data-stu-id="6c1bc-106">true, if the Guid is valid.</span></span>

#### <a name="parameters"></a><span data-ttu-id="6c1bc-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="6c1bc-107">Parameters</span></span>


| <span data-ttu-id="6c1bc-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="6c1bc-108">Parameter</span></span>    | <span data-ttu-id="6c1bc-109">Тип</span><span class="sxs-lookup"><span data-stu-id="6c1bc-109">Type</span></span>    | <span data-ttu-id="6c1bc-110">Описание</span><span class="sxs-lookup"><span data-stu-id="6c1bc-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `guid`    | `string` | <span data-ttu-id="6c1bc-111">Входная строка.</span><span class="sxs-lookup"><span data-stu-id="6c1bc-111">The input string.</span></span> |


