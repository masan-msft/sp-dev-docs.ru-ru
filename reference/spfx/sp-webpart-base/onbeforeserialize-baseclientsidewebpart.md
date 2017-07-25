<span data-ttu-id="64c5a-p101">Этот API вызывается перед сериализацией веб-части. Версия по умолчанию: no-op. Разработчик веб-части может переопределить этот API, когда состояние веб-части отражается в контейнере свойств не полностью, т. е. this.properties. Это позволяет разработчику веб-части обновить контейнер свойств прямо перед сериализацией.</span><span class="sxs-lookup"><span data-stu-id="64c5a-p101">This API is called before the web part is serialized. The default implementation is a no-op. A web part developer can override this API when the web part's state is not fully reflected in the property bag i.e. this.properties. This gives the web part developer a chance to update the property bag right before serialization.</span></span>




Этот API вызывается перед сериализацией веб-части. Версия по умолчанию: no-op. Разработчик веб-части может переопределить этот API, когда состояние веб-части отражается в контейнере свойств не полностью, т. е. this.properties. Это позволяет разработчику веб-части обновить контейнер свойств прямо перед сериализацией.

<span data-ttu-id="64c5a-106">**Подпись:** _@virtual protected onBeforeSerialize(): void;_</span><span class="sxs-lookup"><span data-stu-id="64c5a-106">**Signature:** _@virtual protected onBeforeSerialize(): void;_</span></span>

<span data-ttu-id="64c5a-107">**Возвращаемое значение**: `void`</span><span class="sxs-lookup"><span data-stu-id="64c5a-107">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="64c5a-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="64c5a-108">Parameters</span></span>
<span data-ttu-id="64c5a-109">Нет</span><span class="sxs-lookup"><span data-stu-id="64c5a-109">None</span></span>


