<span data-ttu-id="1db15-p101">Проверяет, равна ли эта версия входному параметру. Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true</span><span class="sxs-lookup"><span data-stu-id="1db15-p101">Checks if this version is equal to the input parameter. Missing patch number is treated as zero. Examples: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true</span></span>




Проверяет, равна ли эта версия входному параметру. Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true

<span data-ttu-id="1db15-105">**Подпись:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="1db15-105">**Signature:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="1db15-106">**Что возвращается**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="1db15-106">**Returns**: `boolean`</span></span>



<span data-ttu-id="1db15-107">Логическое значение, указывающее, равен ли номер версии входному параметру.</span><span class="sxs-lookup"><span data-stu-id="1db15-107">A boolean indicating if this version is equal to the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="1db15-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="1db15-108">Parameters</span></span>


| <span data-ttu-id="1db15-109">Параметр</span><span class="sxs-lookup"><span data-stu-id="1db15-109">Parameter</span></span>    | <span data-ttu-id="1db15-110">Тип</span><span class="sxs-lookup"><span data-stu-id="1db15-110">Type</span></span>    | <span data-ttu-id="1db15-111">Описание</span><span class="sxs-lookup"><span data-stu-id="1db15-111">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="1db15-112">Версия для сравнения</span><span class="sxs-lookup"><span data-stu-id="1db15-112">The version to compare with</span></span> |


