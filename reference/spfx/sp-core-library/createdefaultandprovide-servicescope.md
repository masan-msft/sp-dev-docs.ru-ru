# <a name="createdefaultandprovideservicekey"></a><span data-ttu-id="111d1-101">createDefaultAndProvide(serviceKey)</span><span class="sxs-lookup"><span data-stu-id="111d1-101">createDefaultAndProvide(serviceKey)</span></span>




<span data-ttu-id="111d1-102">Это сокращенная функция, которая создает реализацию по умолчанию для указанного объекта serviceKey, а затем регистрирует ее, вызывая метод ServiceScope.provide().</span><span class="sxs-lookup"><span data-stu-id="111d1-102">This is a shorthand function that constructs the default implementation of the specified serviceKey, and then registers it by calling ServiceScope.provide().</span></span>

<span data-ttu-id="111d1-103">**Подпись:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span><span class="sxs-lookup"><span data-stu-id="111d1-103">**Signature:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span></span>

<span data-ttu-id="111d1-104">**Возвращаемое значение**: `T`</span><span class="sxs-lookup"><span data-stu-id="111d1-104">**Returns**: `T`</span></span>



- <span data-ttu-id="111d1-105">Экземпляр службы, созданный с помощью ServiceKey.defaultCreator</span><span class="sxs-lookup"><span data-stu-id="111d1-105">a service instance that was constructed using ServiceKey.defaultCreator</span></span>

#### <a name="parameters"></a><span data-ttu-id="111d1-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="111d1-106">Parameters</span></span>


| <span data-ttu-id="111d1-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="111d1-107">Parameter</span></span>    | <span data-ttu-id="111d1-108">Тип</span><span class="sxs-lookup"><span data-stu-id="111d1-108">Type</span></span>    | <span data-ttu-id="111d1-109">Описание</span><span class="sxs-lookup"><span data-stu-id="111d1-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="111d1-110">Ключ, который можно применять позже для использования службы</span><span class="sxs-lookup"><span data-stu-id="111d1-110">the key that can be used later to consume the service</span></span> |


