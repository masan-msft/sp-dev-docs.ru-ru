# <a name="createandprovideservicekeysimpleserviceclass"></a>createAndProvide(serviceKey,simpleServiceClass)




Это сокращенная функция, эквивалентная созданию нового экземпляра simpleServiceClass и его регистрации с помощью метода ServiceScope.provide().

**Подпись:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_

**Возвращаемое значение**: `T`



- новый экземпляр класса simpleServiceClass

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Ключ, который можно применять позже для использования службы |
| `simpleServiceClass`    | `{ new (serviceScope: ServiceScope); }` | Создаваемый класс TypeScript |


