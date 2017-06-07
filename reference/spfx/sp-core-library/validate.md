# <a name="validate-class"></a>Класс Validate







Этот класс обеспечивает стандартный способ проверки свойств и параметров функций. В отличие от утверждений отладки, проверки Validate всегда выполняются и всегда возвращают ошибку, даже в рабочей версии. Не злоупотребляйте этими проверками, так как это может повлиять на производительность.






## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`isNonemptyString(value,variableName)`](isnonemptystring-validate.md)     | `public, static` | `void` | Создает исключение, если указанная строка является нулевой, неопределенной или пустой. |
|[`isNotNullOrUndefined(value,variableName)`](isnotnullorundefined-validate.md)     | `public, static` | `void` | Создает исключение, если указано значение null или оно не определено. |
|[`isTrue(value,variableName)`](istrue-validate.md)     | `public, static` | `void` | Создает исключение, если указанное значение не является true. |

## <a name="sample"></a>Пример
```ts
import {
  Validate
} from '@microsoft/sp-core-library';

Validate.isNonemptyString(idValue, "idValue");
Validate.isNotNullOrUndefined(idValue, "idValue");
Validate.isTrue((idValue !== undefined), "idValue");
```
