<span data-ttu-id="1be83-p101">Этот API следует использовать для отображения сообщения об ошибке в области просмотра веб-части. Он также отвечает за запись сообщения об ошибке с помощью средства ведения журнала трассировки.</span><span class="sxs-lookup"><span data-stu-id="1be83-p101">This API should be used to render an error message in the web part display area. Also logs the error message using the trace logger.</span></span>




Этот API следует использовать для отображения сообщения об ошибке в области просмотра веб-части. Он также отвечает за запись сообщения об ошибке с помощью средства ведения журнала трассировки.

<span data-ttu-id="1be83-104">**Подпись:** _protected renderError(error: Error): void;_</span><span class="sxs-lookup"><span data-stu-id="1be83-104">**Signature:** _protected renderError(error: Error): void;_</span></span>

<span data-ttu-id="1be83-105">**Что возвращается**: `void`</span><span class="sxs-lookup"><span data-stu-id="1be83-105">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="1be83-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="1be83-106">Parameters</span></span>


| <span data-ttu-id="1be83-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="1be83-107">Parameter</span></span>    | <span data-ttu-id="1be83-108">Тип</span><span class="sxs-lookup"><span data-stu-id="1be83-108">Type</span></span>    | <span data-ttu-id="1be83-109">Описание</span><span class="sxs-lookup"><span data-stu-id="1be83-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `error`    | `Error` | <span data-ttu-id="1be83-110">Объект ошибки, содержащий сообщение об ошибке для отображения.</span><span class="sxs-lookup"><span data-stu-id="1be83-110">An error object containing the error message to render.</span></span> |


