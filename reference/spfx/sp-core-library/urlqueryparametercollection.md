# <a name="urlqueryparametercollection-class"></a>Класс UrlQueryParameterCollection







Класс для хранения и извлечения параметров запросов. URL-адрес можно указывать относительно сервера, а пустые и нулевые строки будут анализироваться. Первый параметр запроса должен начинаться с символа ?, а все последующие — с символа &. Кроме того, этот класс поддерживает фрагменты. Поведение в крайних случаях: при пустом значении (www.example.com/?test=) сохраняются ключ и пустое значение; если в queryParam нет знаков равенства (www.example.com/?test), сохраняются ключ и неопределенное значение; при пустом queryParam (www.example.com/?&debug=on) сохраняются неопределенные ключ и значение; если параметр запроса содержит только знаки равенства (www.example.com/?=&debug=on), сохраняются пустые ключ и значение строки.


## <a name="constructor"></a>Конструктор


**Подпись:** _constructor(url: string);_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет





## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается    | Описание|
|:-------------|:----|:-------|:-----------|
|[`getValue(param)`](getvalue-urlqueryparametercollection.md)     | `public` | `string` | Возвращает значение первого совпадающего параметра запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> неопределенное значение |
|[`getValues(param)`](getvalues-urlqueryparametercollection.md)     | `public` | `string[]` | Возвращает значения всех совпадающих параметров запроса или неопределенное значение, если ключ не существует. Примеры: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> неопределенное значение |

## <a name="sample"></a>Пример

```ts
import {
  UrlQueryParameterCollection
} from '@microsoft/sp-core-library';

// ...
let queryParameterCollection = new UrlQueryParameterCollection(document.URL);
let idValue = queryParameterCollection.getValue("id");
// ...
```



