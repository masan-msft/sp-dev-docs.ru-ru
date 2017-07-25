# <a name="itimeprovider-interface"></a><span data-ttu-id="e2560-101">Интерфейс ITimeProvider</span><span class="sxs-lookup"><span data-stu-id="e2560-101">ITimeProvider interface</span></span>







<span data-ttu-id="e2560-102">Это интерфейс ServiceScope, который позволяет модульным тестам имитировать системные часы.</span><span class="sxs-lookup"><span data-stu-id="e2560-102">This is a ServiceScope interface that enables unit tests to simulate the system clock.</span></span>







## <a name="methods"></a><span data-ttu-id="e2560-103">Методы</span><span class="sxs-lookup"><span data-stu-id="e2560-103">Methods</span></span>

| <span data-ttu-id="e2560-104">Метод</span><span class="sxs-lookup"><span data-stu-id="e2560-104">Method</span></span>       |  <span data-ttu-id="e2560-105">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="e2560-105">Returns</span></span>   | <span data-ttu-id="e2560-106">Описание</span><span class="sxs-lookup"><span data-stu-id="e2560-106">Description</span></span>|
|:-------------|:-------|:-----------|
|[`getDate()`](getdate-itimeprovider.md)      | `Date` | <span data-ttu-id="e2560-107">Возвращает текущие дату и время.</span><span class="sxs-lookup"><span data-stu-id="e2560-107">Returns the current date/time.</span></span> |
|[`getTimestamp()`](gettimestamp-itimeprovider.md)      | `number` | <span data-ttu-id="e2560-108">Возвращает время DOMHighResTimeStamp, определенное стандартным API performance.now().</span><span class="sxs-lookup"><span data-stu-id="e2560-108">Returns a DOMHighResTimeStamp timing measurement, as defined by the standard performance.now() API.</span></span> |




