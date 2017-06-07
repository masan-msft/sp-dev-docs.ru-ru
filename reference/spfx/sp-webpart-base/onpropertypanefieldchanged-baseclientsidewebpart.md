# <a name="onpropertypanefieldchangedpropertypatholdvaluenewvalue"></a>onPropertyPaneFieldChanged(propertyPath,oldValue,newValue)




Этот API вызывается после обновления нового значения свойства в контейнере свойств, когда PropertyPane используется в режиме Reactive. Базовая версия этого API обновляет веб-часть.

**Подпись:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_

**Возвращаемое значение**: `void`





#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `propertyPath`    | `string` | Путь JSON к свойству в контейнере свойств. |
| `oldValue`    | `any` | Старое значение свойства. |
| `newValue`    | `any` | Новое значение свойства. |


