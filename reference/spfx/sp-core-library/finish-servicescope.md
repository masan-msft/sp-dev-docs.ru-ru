<span data-ttu-id="0035e-p101">Сразу после создания объекта ServiceScope он находится в "незавершенном" состоянии, в котором разрешено вызывать метод provide(), но запрещено вызывать метод consume(). После вызова метода finish() метод consume() будет разрешен, а метод provide() — запрещен. Такой формализм полностью устраняет ряд сложных ошибок, одна из которых описывается ниже. Scope2 — дочерний объект области Scope1, а Scope1 предоставляет экземпляр A1 интерфейса A. Если кто-нибудь использует A1 из Scope2 (путем наследования) перед вызовом метода Scope2.provide() с помощью A2, то при последующем вызове метода Scope2.consume() может возвращаться не такой результат, как при предыдущем. Это может создавать сложности для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0035e-p101">When a ServiceScope is first started, it is in an "unfinished" state where provide() is allowed but consume() is not allowed. After calling finish(), then consume() is allowed but provide() is not allowed. This formalism completely eliminates a number of tricky bugs such as: Scope2 is a child of Scope1, and Scope1 provides instance A1 of interface A; if someone consumes A1 from Scope2 (via inheritance) before Scope2.provide() is called with A2, then a subsequent call to Scope2.consume() might return a different result than the previous call, which would be very confusing for developers.</span></span>




Сразу после создания объекта ServiceScope он находится в "незавершенном" состоянии, в котором разрешено вызывать метод provide(), но запрещено вызывать метод consume(). После вызова метода finish() метод consume() будет разрешен, а метод provide() — запрещен. Такой формализм полностью устраняет ряд сложных ошибок, одна из которых описывается ниже. Scope2 — дочерний объект области Scope1, а Scope1 предоставляет экземпляр A1 интерфейса A. Если кто-нибудь использует A1 из Scope2 (путем наследования) перед вызовом метода Scope2.provide() с помощью A2, то при последующем вызове метода Scope2.consume() может возвращаться не такой результат, как при предыдущем. Это может создавать сложности для разработчиков.

<span data-ttu-id="0035e-105">**Подпись:** _public finish(): void;_</span><span class="sxs-lookup"><span data-stu-id="0035e-105">**Signature:** _public finish(): void;_</span></span>

<span data-ttu-id="0035e-106">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="0035e-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="0035e-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="0035e-107">Parameters</span></span>
<span data-ttu-id="0035e-108">Нет</span><span class="sxs-lookup"><span data-stu-id="0035e-108">None</span></span>


