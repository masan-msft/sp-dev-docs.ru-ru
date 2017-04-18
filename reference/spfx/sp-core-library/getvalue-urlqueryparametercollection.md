# <a name="getvalueparam"></a>getValue(param)




Возвращает значение первого совпадающего параметра запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> неопределенное значение

**Подпись:** _public getValue(param: string): string;_

**Возвращаемое значение**: `string`





#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `param`    | `string` | Ключ (без учета регистра) для необходимого значения параметра запроса. |


