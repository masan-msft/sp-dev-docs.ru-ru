<span data-ttu-id="58ecc-p101">Проверяет, меньше ли эта версия, чем входной параметр (т. е. она является более старой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false</span><span class="sxs-lookup"><span data-stu-id="58ecc-p101">Checks if this version is less (i.e. older) than the input parameter. Missing patch number is treated as zero Examples: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false</span></span>




Проверяет, меньше ли эта версия, чем входной параметр (т. е. она является более старой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false

<span data-ttu-id="58ecc-104">**Подпись:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="58ecc-104">**Signature:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="58ecc-105">**Что возвращается**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="58ecc-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="58ecc-106">Логическое значение, указывающее, ниже ли номер этой версии, чем значение входного параметра.</span><span class="sxs-lookup"><span data-stu-id="58ecc-106">A boolean indicating if this version is less than the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="58ecc-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="58ecc-107">Parameters</span></span>


| <span data-ttu-id="58ecc-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="58ecc-108">Parameter</span></span>    | <span data-ttu-id="58ecc-109">Тип</span><span class="sxs-lookup"><span data-stu-id="58ecc-109">Type</span></span>    | <span data-ttu-id="58ecc-110">Описание</span><span class="sxs-lookup"><span data-stu-id="58ecc-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="58ecc-111">Версия для сравнения</span><span class="sxs-lookup"><span data-stu-id="58ecc-111">The version to compare with</span></span> |


