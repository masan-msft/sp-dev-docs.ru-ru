<span data-ttu-id="fc8e6-p101">Этот API вызывается после обновления нового значения свойства в контейнере свойств, когда PropertyPane используется в режиме Reactive. Базовая версия этого API обновляет веб-часть.</span><span class="sxs-lookup"><span data-stu-id="fc8e6-p101">This API is invoked after updating the new value of the property in the property bag when the PropertyPane is being used in Reactive mode. The base implementation of this API re-renders the web part.</span></span>




Этот API вызывается после обновления нового значения свойства в контейнере свойств, когда PropertyPane используется в режиме Reactive. Базовая версия этого API обновляет веб-часть.

<span data-ttu-id="fc8e6-104">**Подпись:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_</span><span class="sxs-lookup"><span data-stu-id="fc8e6-104">**Signature:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_</span></span>

<span data-ttu-id="fc8e6-105">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="fc8e6-105">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="fc8e6-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="fc8e6-106">Parameters</span></span>


| <span data-ttu-id="fc8e6-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="fc8e6-107">Parameter</span></span>    | <span data-ttu-id="fc8e6-108">Тип</span><span class="sxs-lookup"><span data-stu-id="fc8e6-108">Type</span></span>    | <span data-ttu-id="fc8e6-109">Описание</span><span class="sxs-lookup"><span data-stu-id="fc8e6-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `propertyPath`    | `string` | <span data-ttu-id="fc8e6-110">Путь JSON к свойству в контейнере свойств.</span><span class="sxs-lookup"><span data-stu-id="fc8e6-110">JSON path of the property in the property bag.</span></span> |
| `oldValue`    | `any` | <span data-ttu-id="fc8e6-111">Старое значение свойства.</span><span class="sxs-lookup"><span data-stu-id="fc8e6-111">Old value of the property.</span></span> |
| `newValue`    | `any` | <span data-ttu-id="fc8e6-112">Новое значение свойства.</span><span class="sxs-lookup"><span data-stu-id="fc8e6-112">New value of the property.</span></span> |


