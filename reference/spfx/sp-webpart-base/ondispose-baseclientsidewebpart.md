<span data-ttu-id="80dfd-p101">Этот API можно использовать, чтобы обновить содержимое PropertyPane. Этот API вызывается в конце работы веб-части на странице. Используйте его, чтобы освободить локальные ресурсы (т. е. элементы DOM), которые удерживает веб-часть. Этот API вызывается, когда пользователь переходит с одной страницы основного приложения на другую, и предыдущая страница освобождается.</span><span class="sxs-lookup"><span data-stu-id="80dfd-p101">This API should be used to refresh the contents of the PropertyPane. This API is called at the end of the web part lifecycle on a page. It should be used to dispose any local resources (i.e. DOM elements) that the web part is holding onto. This API is expected to be called in scenarios like page navigation i.e. the host is transitioning from one page to another and disposes the page that is being transitioned out.</span></span>




Этот API можно использовать, чтобы обновить содержимое PropertyPane. Этот API вызывается в конце работы веб-части на странице. Используйте его, чтобы освободить локальные ресурсы (т. е. элементы DOM), которые удерживает веб-часть. Этот API вызывается, когда пользователь переходит с одной страницы основного приложения на другую, и предыдущая страница освобождается.

<span data-ttu-id="80dfd-106">**Подпись:** _@virtual protected onDispose(): void;_</span><span class="sxs-lookup"><span data-stu-id="80dfd-106">**Signature:** _@virtual protected onDispose(): void;_</span></span>

<span data-ttu-id="80dfd-107">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="80dfd-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="80dfd-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="80dfd-108">Parameters</span></span>
<span data-ttu-id="80dfd-109">Нет</span><span class="sxs-lookup"><span data-stu-id="80dfd-109">None</span></span>


