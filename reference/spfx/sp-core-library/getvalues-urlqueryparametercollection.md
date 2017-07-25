<span data-ttu-id="8a228-p101">Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение</span><span class="sxs-lookup"><span data-stu-id="8a228-p101">Returns the values of all of the matching query parameters or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span></span>




Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение

<span data-ttu-id="8a228-104">**Подпись:** _public getValues(param: string): string[];_</span><span class="sxs-lookup"><span data-stu-id="8a228-104">**Signature:** _public getValues(param: string): string[];_</span></span>

<span data-ttu-id="8a228-105">**Возвращаемое значение**: `string[]`</span><span class="sxs-lookup"><span data-stu-id="8a228-105">**Returns**: `string[]`</span></span>





#### <a name="parameters"></a><span data-ttu-id="8a228-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="8a228-106">Parameters</span></span>


| <span data-ttu-id="8a228-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="8a228-107">Parameter</span></span>    | <span data-ttu-id="8a228-108">Тип</span><span class="sxs-lookup"><span data-stu-id="8a228-108">Type</span></span>    | <span data-ttu-id="8a228-109">Описание</span><span class="sxs-lookup"><span data-stu-id="8a228-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `param`    | `string` | <span data-ttu-id="8a228-110">Ключ (без учета регистра) для необходимого значения параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="8a228-110">the case insensitive key for the desired query parameter value.</span></span> |


