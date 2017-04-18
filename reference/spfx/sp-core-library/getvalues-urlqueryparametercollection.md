# <a name="getvaluesparam"></a>getValues(param)




Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение

**Подпись:** _public getValues(param: string): string[];_

**Возвращаемое значение**: `string[]`





#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `param`    | `string` | Ключ (без учета регистра) для необходимого значения параметра запроса. |


