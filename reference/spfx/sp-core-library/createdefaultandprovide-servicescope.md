# <a name="createdefaultandprovideservicekey"></a>createDefaultAndProvide(serviceKey)




Это сокращенная функция, которая создает реализацию по умолчанию для указанного объекта serviceKey, а затем регистрирует ее, вызывая метод ServiceScope.provide().

**Подпись:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_

**Возвращаемое значение**: `T`



- Экземпляр службы, созданный с помощью ServiceKey.defaultCreator

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Ключ, который можно применять позже для использования службы |


