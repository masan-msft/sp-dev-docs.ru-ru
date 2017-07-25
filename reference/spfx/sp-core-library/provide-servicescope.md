<span data-ttu-id="7dfce-p101">Метод ServiceScope.provide() позволяет зарегистрировать версию определенного объекта serviceKey для текущей области. Его можно использовать, только когда ServiceScope находится в "незавершенном" состоянии, т. е. до вызова метода finish().</span><span class="sxs-lookup"><span data-stu-id="7dfce-p101">ServiceScope.provide() is used to register an implemententation of the given serviceKey for the current scope. It may only be used when the ServiceScope is in an "unfinished" state, i.e. before finish() has been called.</span></span>




Метод ServiceScope.provide() позволяет зарегистрировать версию определенного объекта serviceKey для текущей области. Его можно использовать, только когда ServiceScope находится в "незавершенном" состоянии, т. е. до вызова метода finish().

<span data-ttu-id="7dfce-104">**Подпись:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_</span><span class="sxs-lookup"><span data-stu-id="7dfce-104">**Signature:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_</span></span>

<span data-ttu-id="7dfce-105">**Возвращаемое значение**: `T`</span><span class="sxs-lookup"><span data-stu-id="7dfce-105">**Returns**: `T`</span></span>



- <span data-ttu-id="7dfce-106">тот же объект, который передавался в качестве параметра service</span><span class="sxs-lookup"><span data-stu-id="7dfce-106">the same object that was passed as the "service" parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="7dfce-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="7dfce-107">Parameters</span></span>


| <span data-ttu-id="7dfce-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="7dfce-108">Parameter</span></span>    | <span data-ttu-id="7dfce-109">Тип</span><span class="sxs-lookup"><span data-stu-id="7dfce-109">Type</span></span>    | <span data-ttu-id="7dfce-110">Описание</span><span class="sxs-lookup"><span data-stu-id="7dfce-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="7dfce-111">Ключ, который в дальнейшем будет применяться для использования службы.</span><span class="sxs-lookup"><span data-stu-id="7dfce-111">the key that will later be used to consume the service</span></span> |
| `service`    | `T` | <span data-ttu-id="7dfce-112">Регистрируемый экземпляр службы</span><span class="sxs-lookup"><span data-stu-id="7dfce-112">the service instance that is being registered</span></span> |


