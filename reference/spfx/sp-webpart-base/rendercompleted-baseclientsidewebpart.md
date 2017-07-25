<span data-ttu-id="bab6a-p101">Этот API должен вызываться веб-частями, которые выполняют асинхронную отрисовку. Эти веб-части должны переопределять API isRenderAsync и возвращать значение true. Пример: веб-части, которые отрисовывают содержимое в окне IFrame. Веб-часть инициирует отрисовку IFrame в API render(), но фактически отрисовка завершается только после загрузки окна iframe.</span><span class="sxs-lookup"><span data-stu-id="bab6a-p101">This API should be called by web parts that perform Async rendering. Those web part are required to override the isRenderAsync API and return true. One such example is web parts that render content in an IFrame. The web part initiates the IFrame rendering in the render() API but the actual rendering is complete only after the iframe loading completes.</span></span>




Этот API должен вызываться веб-частями, которые выполняют асинхронную отрисовку. Эти веб-части должны переопределять API isRenderAsync и возвращать значение true. Пример: веб-части, которые отрисовывают содержимое в окне IFrame. Веб-часть инициирует отрисовку IFrame в API render(), но фактически отрисовка завершается только после загрузки окна iframe.

<span data-ttu-id="bab6a-106">**Подпись:** _protected renderCompleted(): void;_</span><span class="sxs-lookup"><span data-stu-id="bab6a-106">**Signature:** _protected renderCompleted(): void;_</span></span>

<span data-ttu-id="bab6a-107">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="bab6a-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="bab6a-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="bab6a-108">Parameters</span></span>
<span data-ttu-id="bab6a-109">Нет</span><span class="sxs-lookup"><span data-stu-id="bab6a-109">None</span></span>


