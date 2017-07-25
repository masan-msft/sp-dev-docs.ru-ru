<span data-ttu-id="bbd1f-p103">Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение</span><span class="sxs-lookup"><span data-stu-id="bbd1f-p103">Returns the values of all of the matching query parameters or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span></span> |
|[`getValues(param)`](getvalues-urlqueryparametercollection.md)     | `public` | `string[]` | Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение |

## <a name="sample"></a><span data-ttu-id="bbd1f-122">Пример</span><span class="sxs-lookup"><span data-stu-id="bbd1f-122">Sample</span></span>

```ts
import {
  UrlQueryParameterCollection
} from '@microsoft/sp-core-library';

// ...
let queryParameterCollection = new UrlQueryParameterCollection(document.URL);
let idValue = queryParameterCollection.getValue("id");
// ...
```



