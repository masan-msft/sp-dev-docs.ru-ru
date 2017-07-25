<span data-ttu-id="bb55c-p101">Создает новый экземпляр Version с помощью строки версии. Метод tryParse проверяет входную строку версии и возвращает ошибку, если она является недопустимой.</span><span class="sxs-lookup"><span data-stu-id="bb55c-p101">Constructs a new Version instance using the version string. tryParse validates the input version string and throws error if it is invalid</span></span>




Создает новый экземпляр Version с помощью строки версии. Метод tryParse проверяет входную строку версии и возвращает ошибку, если она является недопустимой.

<span data-ttu-id="bb55c-104">**Подпись:** _public static parse(versionString: string): [Version](../sp-core-library/version.md);_</span><span class="sxs-lookup"><span data-stu-id="bb55c-104">**Signature:** _public static parse(versionString: string): [Version](../sp-core-library/version.md);_</span></span>

<span data-ttu-id="bb55c-105">**Возвращаемое значение**: [`Version`](../sp-core-library/version.md)</span><span class="sxs-lookup"><span data-stu-id="bb55c-105">**Returns**: [`Version`](../sp-core-library/version.md)</span></span>



<span data-ttu-id="bb55c-106">Новый экземпляр Version (если он является допустимым)</span><span class="sxs-lookup"><span data-stu-id="bb55c-106">If valid, a new Version instace</span></span>

#### <a name="parameters"></a><span data-ttu-id="bb55c-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="bb55c-107">Parameters</span></span>


| <span data-ttu-id="bb55c-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="bb55c-108">Parameter</span></span>    | <span data-ttu-id="bb55c-109">Тип</span><span class="sxs-lookup"><span data-stu-id="bb55c-109">Type</span></span>    | <span data-ttu-id="bb55c-110">Описание</span><span class="sxs-lookup"><span data-stu-id="bb55c-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `versionString`    | `string` | <span data-ttu-id="bb55c-111">Строка версии</span><span class="sxs-lookup"><span data-stu-id="bb55c-111">A version string</span></span> |


