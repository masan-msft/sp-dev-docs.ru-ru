<span data-ttu-id="fecdf-p101">Если вызвать метод ServiceScope.consume() до вызова метода finish(), возникнет ошибка. Самый надежный способ защитить компонент от этой ошибки — вызывать метод consume() из функции обратного вызова whenFinished(). Если область службы уже готова, обратный вызов будет выполнен немедленно. В противном случае он будет выполнен позже, когда создание области будет завершено.</span><span class="sxs-lookup"><span data-stu-id="fecdf-p101">It is an error to call ServiceScope.consume() before finish() has been called. The most reliable way to protect your component against this error is to perform the consume() calls inside a whenFinished() callback. If the service scope is already finished, then the callback will be executed immediately; otherwise, it will be executed later when the scope is finished.</span></span>




Если вызвать метод ServiceScope.consume() до вызова метода finish(), возникнет ошибка. Самый надежный способ защитить компонент от этой ошибки — вызывать метод consume() из функции обратного вызова whenFinished(). Если область службы уже готова, обратный вызов будет выполнен немедленно. В противном случае он будет выполнен позже, когда создание области будет завершено.

<span data-ttu-id="fecdf-105">**Подпись:** _public whenFinished(callback: () => void): void;_</span><span class="sxs-lookup"><span data-stu-id="fecdf-105">**Signature:** _public whenFinished(callback: () => void): void;_</span></span>

<span data-ttu-id="fecdf-106">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="fecdf-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="fecdf-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="fecdf-107">Parameters</span></span>


| <span data-ttu-id="fecdf-108">Параметр</span><span class="sxs-lookup"><span data-stu-id="fecdf-108">Parameter</span></span>    | <span data-ttu-id="fecdf-109">Тип</span><span class="sxs-lookup"><span data-stu-id="fecdf-109">Type</span></span>    | <span data-ttu-id="fecdf-110">Описание</span><span class="sxs-lookup"><span data-stu-id="fecdf-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `callback`    | `() => void` | <span data-ttu-id="fecdf-111">Блок кода, который должен вызывать метод ServiceScope.consume()</span><span class="sxs-lookup"><span data-stu-id="fecdf-111">A block of code that needs to call ServiceScope.consume()</span></span> |


