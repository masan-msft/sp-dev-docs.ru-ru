# <a name="createnameserviceclass"></a>create(name,serviceClass)




Создает новый объект ServiceKey, версией по умолчанию которого будет новый экземпляр класса TypeScript, принимающий стандартный параметр конструктора. Чтобы указать пользовательские параметры конструктора, используйте метод createCustom().

**Подпись:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_

**Возвращаемое значение**: [`ServiceKey`](../sp-core-library/servicekey.md)<T>



- Новый объект ServiceKey

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `name`    | `string` | Имя, например "MyApplication.IMyService", которое должно быть уникальным в приложении. |
| `serviceClass`    | `{ new (serviceScope: ServiceScope); }` | Класс TypeScript, реализующий службу. |


