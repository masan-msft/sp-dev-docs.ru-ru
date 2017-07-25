<span data-ttu-id="603b9-p101">Этот API вызывается после завершения настройки PropertyPane. Он вызывается в следующих случаях: – Когда истекает время CONFIGURATION_COMPLETE_TIMEOUT((текущее значение — 5 секунд) после последнего изменения. – Когда пользователь нажимает кнопку "x" (закрыть) до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь нажимает кнопку "Применить" до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь открывает другую веб-часть, тогда текущая веб-часть получает это событие.</span><span class="sxs-lookup"><span data-stu-id="603b9-p101">This API is invoked when the configuration is completed on the PropertyPane. It's invoked in the following cases: - When the CONFIGURATION_COMPLETE_TIMEOUT((currently the value is 5 secs) elapses after the last change. - When user clicks 'x'(close) button before the CONFIGURATION_COMPLETE_TIMEOUT elapses. - When user clciks 'Apply' button before the CONFIGURATION_COMPLETE_TIMEOUT elapses. - When the user switches web parts then the current web part gets this event.</span></span>




Этот API вызывается после завершения настройки PropertyPane. Он вызывается в следующих случаях: – Когда истекает время CONFIGURATION_COMPLETE_TIMEOUT((текущее значение — 5 секунд) после последнего изменения. – Когда пользователь нажимает кнопку "x" (закрыть) до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь нажимает кнопку "Применить" до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь открывает другую веб-часть, тогда текущая веб-часть получает это событие.

<span data-ttu-id="603b9-107">**Подпись:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_</span><span class="sxs-lookup"><span data-stu-id="603b9-107">**Signature:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_</span></span>

<span data-ttu-id="603b9-108">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="603b9-108">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="603b9-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="603b9-109">Parameters</span></span>
<span data-ttu-id="603b9-110">Нет</span><span class="sxs-lookup"><span data-stu-id="603b9-110">None</span></span>


