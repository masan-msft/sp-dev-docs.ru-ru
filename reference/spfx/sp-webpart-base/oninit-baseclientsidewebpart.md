<span data-ttu-id="8d720-p101">Этот API следует переопределять для выполнения длительных операций, например получения данных от удаленной службы перед начальной отрисовкой веб-части. Во время работы этого метода отображается индикатор загрузки. Этот API вызывается только один раз во время работы веб-части.</span><span class="sxs-lookup"><span data-stu-id="8d720-p101">This API should be overridden to perform long running operations e.g. data fetching from a remote service before the initial rendering of the web part. The loading indicator is displayed during the lifetime of this method. This API is called only once during the lifecycle of a web part.</span></span>




Этот API следует переопределять для выполнения длительных операций, например получения данных от удаленной службы перед начальной отрисовкой веб-части. Во время работы этого метода отображается индикатор загрузки. Этот API вызывается только один раз во время работы веб-части.

<span data-ttu-id="8d720-105">**Подпись:** _@virtual protected onInit(): Promise<void>;_</span><span class="sxs-lookup"><span data-stu-id="8d720-105">**Signature:** _@virtual protected onInit(): Promise<void>;_</span></span>

<span data-ttu-id="8d720-106">**Возвращаемое значение**: `Promise<void>`</span><span class="sxs-lookup"><span data-stu-id="8d720-106">**Returns**: `Promise<void>`</span></span>





#### <a name="parameters"></a><span data-ttu-id="8d720-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="8d720-107">Parameters</span></span>
<span data-ttu-id="8d720-108">Нет</span><span class="sxs-lookup"><span data-stu-id="8d720-108">None</span></span>


