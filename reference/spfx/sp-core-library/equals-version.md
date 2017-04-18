# <a name="equalscomparewith"></a>equals(compareWith)




Проверяет, равна ли эта версия входному параметру. Если номер исправления отсутствует, он приравнивается к нулю. Примеры: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true

**Подпись:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Что возвращается**: `boolean`



Логическое значение, указывающее, равен ли номер версии входному параметру.

#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Версия для сравнения |


