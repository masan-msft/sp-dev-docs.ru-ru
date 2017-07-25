<span data-ttu-id="bfa29-p101">Этот класс обеспечивает стандартный способ проверки свойств и параметров функций. В отличие от утверждений отладки, проверки Validate всегда выполняются и всегда возвращают ошибку, даже в рабочей версии. Не злоупотребляйте этими проверками, так как это может повлиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="bfa29-p101">This class implements provides a standard way to validate properties and function parameters. Unlike debug assertions, Validate checks are always performed and will always throw an error, even in a production release. As such, be careful not to overuse these checks in a way that might impact performance.</span></span>







Этот класс обеспечивает стандартный способ проверки свойств и параметров функций. В отличие от утверждений отладки, проверки Validate всегда выполняются и всегда возвращают ошибку, даже в рабочей версии. Не злоупотребляйте этими проверками, так как это может повлиять на производительность.






## <a name="methods"></a><span data-ttu-id="bfa29-105">Методы</span><span class="sxs-lookup"><span data-stu-id="bfa29-105">Methods</span></span>

| <span data-ttu-id="bfa29-106">Метод</span><span class="sxs-lookup"><span data-stu-id="bfa29-106">Method</span></span>       | <span data-ttu-id="bfa29-107">Модификатор доступа</span><span class="sxs-lookup"><span data-stu-id="bfa29-107">Access Modifier</span></span> | <span data-ttu-id="bfa29-108">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="bfa29-108">Returns</span></span>  | <span data-ttu-id="bfa29-109">Описание</span><span class="sxs-lookup"><span data-stu-id="bfa29-109">Description</span></span>|
|:-------------|:----|:-------|:-----------|
|[`isNonemptyString(value,variableName)`](isnonemptystring-validate.md)     | `public, static` | `void` | <span data-ttu-id="bfa29-110">Создает исключение, если указанная строка является нулевой, неопределенной или пустой.</span><span class="sxs-lookup"><span data-stu-id="bfa29-110">Throws an exception if the specified string is null, undefined, or an empty string.</span></span> |
|[`isNotNullOrUndefined(value,variableName)`](isnotnullorundefined-validate.md)     | `public, static` | `void` | <span data-ttu-id="bfa29-111">Создает исключение, если указано значение null или оно не определено.</span><span class="sxs-lookup"><span data-stu-id="bfa29-111">Throws an exception if the specified value is null or undefined.</span></span> |
|[`isTrue(value,variableName)`](istrue-validate.md)     | `public, static` | `void` | <span data-ttu-id="bfa29-112">Создает исключение, если указанное значение не является true.</span><span class="sxs-lookup"><span data-stu-id="bfa29-112">Throws an exception if the specified value is not true.</span></span> |

## <a name="sample"></a><span data-ttu-id="bfa29-113">Пример</span><span class="sxs-lookup"><span data-stu-id="bfa29-113">Sample</span></span>
```ts
import {
  Validate
} from '@microsoft/sp-core-library';

Validate.isNonemptyString(idValue, "idValue");
Validate.isNotNullOrUndefined(idValue, "idValue");
Validate.isTrue((idValue !== undefined), "idValue");
```
