# <a name="createandprovideservicekeysimpleserviceclass"></a><span data-ttu-id="2a5fd-101">createAndProvide(serviceKey,simpleServiceClass)</span><span class="sxs-lookup"><span data-stu-id="2a5fd-101">createAndProvide(serviceKey,simpleServiceClass)</span></span>




<span data-ttu-id="2a5fd-102">Это сокращенная функция, эквивалентная созданию нового экземпляра simpleServiceClass и его регистрации с помощью метода ServiceScope.provide().</span><span class="sxs-lookup"><span data-stu-id="2a5fd-102">This is a shorthand function that its equivalent to constructing a new instance of the simpleServiceClass, then registering it by calling ServiceScope.provide().</span></span>

<span data-ttu-id="2a5fd-103">**Подпись:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_</span><span class="sxs-lookup"><span data-stu-id="2a5fd-103">**Signature:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_</span></span>

<span data-ttu-id="2a5fd-104">**Возвращаемое значение**: `T`</span><span class="sxs-lookup"><span data-stu-id="2a5fd-104">**Returns**: `T`</span></span>



- <span data-ttu-id="2a5fd-105">новый экземпляр класса simpleServiceClass</span><span class="sxs-lookup"><span data-stu-id="2a5fd-105">a newly constructed instance of simpleServiceClass</span></span>

#### <a name="parameters"></a><span data-ttu-id="2a5fd-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="2a5fd-106">Parameters</span></span>


| <span data-ttu-id="2a5fd-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="2a5fd-107">Parameter</span></span>    | <span data-ttu-id="2a5fd-108">Тип</span><span class="sxs-lookup"><span data-stu-id="2a5fd-108">Type</span></span>    | <span data-ttu-id="2a5fd-109">Описание</span><span class="sxs-lookup"><span data-stu-id="2a5fd-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="2a5fd-110">Ключ, который можно применять позже для использования службы</span><span class="sxs-lookup"><span data-stu-id="2a5fd-110">the key that can be used later to consume the service</span></span> |
| `simpleServiceClass`    | `{ new (serviceScope: ServiceScope); }` | <span data-ttu-id="2a5fd-111">Создаваемый класс TypeScript</span><span class="sxs-lookup"><span data-stu-id="2a5fd-111">the TypeScript class to be constructed</span></span> |


