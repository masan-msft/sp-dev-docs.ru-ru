# <a name="itimeprovider-interface"></a>Интерфейс ITimeProvider







Это интерфейс ServiceScope, который позволяет модульным тестам имитировать системные часы.







## <a name="methods"></a>Методы

| Метод       |  Что возвращается   | Описание|
|:-------------|:-------|:-----------|
|[`getDate()`](getdate-itimeprovider.md)      | `Date` | Возвращает текущие дату и время. |
|[`getTimestamp()`](gettimestamp-itimeprovider.md)      | `number` | Возвращает время DOMHighResTimeStamp, определенное стандартным API performance.now(). |




