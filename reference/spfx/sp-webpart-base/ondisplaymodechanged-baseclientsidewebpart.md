<span data-ttu-id="9ec7b-p101">Этот API вызывается при изменении режима отображения веб-части. Версия этого API по умолчанию вызывает метод render, чтобы обновить веб-часть. Если разработчик веб-части не хочет, чтобы после изменения режима отображения происходило полное обновление, он может переопределить этот API и выполнить обновления модели DOM веб-части, чтобы изменить режим отображения.</span><span class="sxs-lookup"><span data-stu-id="9ec7b-p101">This API is called when the display mode of a web part is changed. The default implementation of this API calls the web part render method to re-render the web part with the new display mode. If a web part developer does not want a full re-render to happen on display mode change, they can override this API and perform specific updates to the web part DOM to switch its display mode.</span></span>




Этот API вызывается при изменении режима отображения веб-части. Версия этого API по умолчанию вызывает метод render, чтобы обновить веб-часть. Если разработчик веб-части не хочет, чтобы после изменения режима отображения происходило полное обновление, он может переопределить этот API и выполнить обновления модели DOM веб-части, чтобы изменить режим отображения.

<span data-ttu-id="9ec7b-105">**Подпись:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_</span><span class="sxs-lookup"><span data-stu-id="9ec7b-105">**Signature:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_</span></span>

<span data-ttu-id="9ec7b-106">**Что возвращается**: `void`</span><span class="sxs-lookup"><span data-stu-id="9ec7b-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="9ec7b-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="9ec7b-107">Parameters</span></span>


| <span data-ttu-id="9ec7b-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ec7b-108">Parameter</span></span>    | <span data-ttu-id="9ec7b-109">Тип</span><span class="sxs-lookup"><span data-stu-id="9ec7b-109">Type</span></span>    | <span data-ttu-id="9ec7b-110">Описание</span><span class="sxs-lookup"><span data-stu-id="9ec7b-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `oldDisplayMode`    | [`DisplayMode`](../sp-core-library/displaymode.md) | <span data-ttu-id="9ec7b-111">Старый режим отображения.</span><span class="sxs-lookup"><span data-stu-id="9ec7b-111">The old display mode.</span></span> |


