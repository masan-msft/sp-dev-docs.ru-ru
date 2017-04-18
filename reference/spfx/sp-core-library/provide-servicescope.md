# <a name="provideservicekeyservice"></a>provide(serviceKey,service)




Метод ServiceScope.provide() позволяет зарегистрировать версию определенного объекта serviceKey для текущей области. Его можно использовать, только когда ServiceScope находится в "незавершенном" состоянии, т. е. до вызова метода finish().

**Подпись:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_

**Возвращаемое значение**: `T`



- тот же объект, который передавался в качестве параметра service

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Ключ, который в дальнейшем будет применяться для использования службы. |
| `service`    | `T` | Регистрируемый экземпляр службы |


