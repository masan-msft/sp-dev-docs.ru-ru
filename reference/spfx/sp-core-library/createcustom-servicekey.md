# <a name="createcustomnamedefaultcreator"></a><span data-ttu-id="6a9e2-101">createCustom(name,defaultCreator)</span><span class="sxs-lookup"><span data-stu-id="6a9e2-101">createCustom(name,defaultCreator)</span></span>




<span data-ttu-id="6a9e2-102">Создает новый объект ServiceKey, реализацию по умолчанию для которого можно получить с помощью указанного метода обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="6a9e2-102">Constructs a new ServiceKey whose default implementation will be obtained by invoking the specified callback.</span></span>

<span data-ttu-id="6a9e2-103">**Подпись:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span><span class="sxs-lookup"><span data-stu-id="6a9e2-103">**Signature:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span></span>

<span data-ttu-id="6a9e2-104">**Возвращаемое значение**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span><span class="sxs-lookup"><span data-stu-id="6a9e2-104">**Returns**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span></span>



- <span data-ttu-id="6a9e2-105">Новый объект ServiceKey</span><span class="sxs-lookup"><span data-stu-id="6a9e2-105">the newly created ServiceKey</span></span>

#### <a name="parameters"></a><span data-ttu-id="6a9e2-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="6a9e2-106">Parameters</span></span>


| <span data-ttu-id="6a9e2-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="6a9e2-107">Parameter</span></span>    | <span data-ttu-id="6a9e2-108">Тип</span><span class="sxs-lookup"><span data-stu-id="6a9e2-108">Type</span></span>    | <span data-ttu-id="6a9e2-109">Описание</span><span class="sxs-lookup"><span data-stu-id="6a9e2-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `name`    | `string` | <span data-ttu-id="6a9e2-110">Имя, например "MyApplication.IMyService", которое должно быть уникальным в приложении.</span><span class="sxs-lookup"><span data-stu-id="6a9e2-110">A name such as "MyApplication.IMyService" which should be unique within your application.</span></span> |
| `defaultCreator`    | `ServiceCreator<T>` | <span data-ttu-id="6a9e2-111">Обратный вызов, который возвращает объект, реализующий интерфейс T.</span><span class="sxs-lookup"><span data-stu-id="6a9e2-111">A callback that returns an object that implements the T interface</span></span> |


