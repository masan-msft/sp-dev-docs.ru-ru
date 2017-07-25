<span data-ttu-id="5c17a-p101">Создает новый объект ServiceKey, версией по умолчанию которого будет новый экземпляр класса TypeScript, принимающий стандартный параметр конструктора. Чтобы указать пользовательские параметры конструктора, используйте метод createCustom().</span><span class="sxs-lookup"><span data-stu-id="5c17a-p101">Constructs a new ServiceKey whose default implementation will be a new instance of a TypeScript class that accepts the standard constructor parameter. If you want to specify custom constructor parameters, use createCustom() instead.</span></span>




Создает новый объект ServiceKey, версией по умолчанию которого будет новый экземпляр класса TypeScript, принимающий стандартный параметр конструктора. Чтобы указать пользовательские параметры конструктора, используйте метод createCustom().

<span data-ttu-id="5c17a-104">**Подпись:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span><span class="sxs-lookup"><span data-stu-id="5c17a-104">**Signature:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span></span>

<span data-ttu-id="5c17a-105">**Возвращаемое значение**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span><span class="sxs-lookup"><span data-stu-id="5c17a-105">**Returns**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span></span>



- <span data-ttu-id="5c17a-106">Новый объект ServiceKey</span><span class="sxs-lookup"><span data-stu-id="5c17a-106">the newly created ServiceKey</span></span>

#### <a name="parameters"></a><span data-ttu-id="5c17a-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c17a-107">Parameters</span></span>


| <span data-ttu-id="5c17a-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="5c17a-108">Parameter</span></span>    | <span data-ttu-id="5c17a-109">Тип</span><span class="sxs-lookup"><span data-stu-id="5c17a-109">Type</span></span>    | <span data-ttu-id="5c17a-110">Описание</span><span class="sxs-lookup"><span data-stu-id="5c17a-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `name`    | `string` | <span data-ttu-id="5c17a-111">Имя, например "MyApplication.IMyService", которое должно быть уникальным в приложении.</span><span class="sxs-lookup"><span data-stu-id="5c17a-111">A name such as "MyApplication.IMyService" which should be unique within your application.</span></span> |
| `serviceClass`    | `{ new (serviceScope: ServiceScope); }` | <span data-ttu-id="5c17a-112">Класс TypeScript, реализующий службу.</span><span class="sxs-lookup"><span data-stu-id="5c17a-112">the TypeScript class that implements the service.</span></span> |


