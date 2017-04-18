# <a name="createcustomnamedefaultcreator"></a>createCustom(name,defaultCreator)




Создает новый объект ServiceKey, реализацию по умолчанию для которого можно получить с помощью указанного метода обратного вызова.

**Подпись:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_

**Возвращаемое значение**: [`ServiceKey`](../sp-core-library/servicekey.md)<T>



- Новый объект ServiceKey

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `name`    | `string` | Имя, например "MyApplication.IMyService", которое должно быть уникальным в приложении. |
| `defaultCreator`    | `ServiceCreator<T>` | Обратный вызов, который возвращает объект, реализующий интерфейс T. |


