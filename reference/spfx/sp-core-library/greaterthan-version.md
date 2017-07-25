<span data-ttu-id="05200-p101">Проверяет, больше ли эта версия, чем входной параметр (т. е. она является более новой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true</span><span class="sxs-lookup"><span data-stu-id="05200-p101">Checks if this version is greater (i.e. newer) than the input parameter. Missing patch number is treated as zero Examples: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true</span></span>




Проверяет, больше ли эта версия, чем входной параметр (т. е. она является более новой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true

<span data-ttu-id="05200-104">**Подпись:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="05200-104">**Signature:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="05200-105">**Что возвращается**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="05200-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="05200-106">Логическое значение, указывающее, превышает ли номер этой версии значение входного параметра.</span><span class="sxs-lookup"><span data-stu-id="05200-106">A boolean indicating if this version is greater than the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="05200-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="05200-107">Parameters</span></span>


| <span data-ttu-id="05200-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="05200-108">Parameter</span></span>    | <span data-ttu-id="05200-109">Тип</span><span class="sxs-lookup"><span data-stu-id="05200-109">Type</span></span>    | <span data-ttu-id="05200-110">Описание</span><span class="sxs-lookup"><span data-stu-id="05200-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="05200-111">Версия для сравнения</span><span class="sxs-lookup"><span data-stu-id="05200-111">The version to compare with</span></span> |


