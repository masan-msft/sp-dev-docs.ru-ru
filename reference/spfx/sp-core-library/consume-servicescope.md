<span data-ttu-id="b64a0-p101">Компоненты должны вызывать эту функцию для "использования" зависимости, т. е. поиска serviceKey и возвращения зарегистрированного экземпляра службы. Если найти экземпляр не удается, будет автоматически создан и зарегистрирован экземпляр по умолчанию с корневым объектом ServiceScope.</span><span class="sxs-lookup"><span data-stu-id="b64a0-p101">Components should call this function to "consume" a dependency, i.e. look up the serviceKey and return the registered service instance. If the instance cannot be found, then a default instance will be autocreated and registered with the root ServiceScope.</span></span>




Компоненты должны вызывать эту функцию для "использования" зависимости, т. е. поиска serviceKey и возвращения зарегистрированного экземпляра службы. Если найти экземпляр не удается, будет автоматически создан и зарегистрирован экземпляр по умолчанию с корневым объектом ServiceScope.

<span data-ttu-id="b64a0-104">**Подпись:** _public consume < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span><span class="sxs-lookup"><span data-stu-id="b64a0-104">**Signature:** _public consume < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span></span>

<span data-ttu-id="b64a0-105">**Возвращаемое значение**: `T`</span><span class="sxs-lookup"><span data-stu-id="b64a0-105">**Returns**: `T`</span></span>



- <span data-ttu-id="b64a0-106">Экземпляр службы</span><span class="sxs-lookup"><span data-stu-id="b64a0-106">the service instance</span></span>

#### <a name="parameters"></a><span data-ttu-id="b64a0-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="b64a0-107">Parameters</span></span>


| <span data-ttu-id="b64a0-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="b64a0-108">Parameter</span></span>    | <span data-ttu-id="b64a0-109">Тип</span><span class="sxs-lookup"><span data-stu-id="b64a0-109">Type</span></span>    | <span data-ttu-id="b64a0-110">Описание</span><span class="sxs-lookup"><span data-stu-id="b64a0-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="b64a0-111">Ключ, который использовался при вызове метода provide() для регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="b64a0-111">the key that was used when provide() was called to register the service</span></span> |


