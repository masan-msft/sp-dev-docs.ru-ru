# <a name="greaterthancomparewith"></a>greaterThan(compareWith)




Проверяет, больше ли эта версия, чем входной параметр (т. е. она является более новой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true

**Подпись:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Что возвращается**: `boolean`



Логическое значение, указывающее, превышает ли номер этой версии значение входного параметра.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Версия для сравнения |


