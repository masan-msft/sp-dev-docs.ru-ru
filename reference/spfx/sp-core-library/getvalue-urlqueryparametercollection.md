<span data-ttu-id="b8697-p101">Возвращает значение первого совпадающего параметра запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> неопределенное значение</span><span class="sxs-lookup"><span data-stu-id="b8697-p101">Returns the value of the first matching query parameter or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined</span></span>




Возвращает значение первого совпадающего параметра запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> неопределенное значение

<span data-ttu-id="b8697-104">**Подпись:** _public getValue(param: string): string;_</span><span class="sxs-lookup"><span data-stu-id="b8697-104">**Signature:** _public getValue(param: string): string;_</span></span>

<span data-ttu-id="b8697-105">**Возвращаемое значение**: `string`</span><span class="sxs-lookup"><span data-stu-id="b8697-105">**Returns**: `string`</span></span>





#### <a name="parameters"></a><span data-ttu-id="b8697-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="b8697-106">Parameters</span></span>


| <span data-ttu-id="b8697-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="b8697-107">Parameter</span></span>    | <span data-ttu-id="b8697-108">Тип</span><span class="sxs-lookup"><span data-stu-id="b8697-108">Type</span></span>    | <span data-ttu-id="b8697-109">Описание</span><span class="sxs-lookup"><span data-stu-id="b8697-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `param`    | `string` | <span data-ttu-id="b8697-110">Ключ (без учета регистра) для необходимого значения параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="b8697-110">the case insensitive key for the desired query parameter value.</span></span> |


