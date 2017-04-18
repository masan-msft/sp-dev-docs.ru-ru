# <a name="lessthancomparewith"></a>lessThan(compareWith)




Проверяет, меньше ли эта версия, чем входной параметр (т. е. она является более старой). Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false

**Подпись:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Что возвращается**: `boolean`



Логическое значение, указывающее, ниже ли номер этой версии, чем значение входного параметра.

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Версия для сравнения |


