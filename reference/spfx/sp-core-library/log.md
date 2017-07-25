<span data-ttu-id="1ef02-p101">Класс Log предоставляет статические методы для ведения журнала сообщений на различных уровнях (подробности, информация, предупреждение, ошибка) и с контекстной информацией. Контекстная информация помогает определить, какой компонент создал сообщения, делает сообщения полезными и позволяет фильтровать их.</span><span class="sxs-lookup"><span data-stu-id="1ef02-p101">The Log class provides static methods for logging messages at different levels (verbose, info, warning, error) and with context information. Context information helps identify which component generated the messages and makes the messages useful and filterable.</span></span>







Класс Log предоставляет статические методы для ведения журнала сообщений на различных уровнях (подробности, информация, предупреждение, ошибка) и с контекстной информацией. Контекстная информация помогает определить, какой компонент создал сообщения, делает сообщения полезными и позволяет фильтровать их.






## <a name="methods"></a><span data-ttu-id="1ef02-104">Методы</span><span class="sxs-lookup"><span data-stu-id="1ef02-104">Methods</span></span>

| <span data-ttu-id="1ef02-105">Метод</span><span class="sxs-lookup"><span data-stu-id="1ef02-105">Method</span></span>       | <span data-ttu-id="1ef02-106">Модификатор доступа</span><span class="sxs-lookup"><span data-stu-id="1ef02-106">Access Modifier</span></span> | <span data-ttu-id="1ef02-107">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="1ef02-107">Returns</span></span>  | <span data-ttu-id="1ef02-108">Описание</span><span class="sxs-lookup"><span data-stu-id="1ef02-108">Description</span></span>|
|:-------------|:----|:-------|:-----------|
|[`error(source,error,scope)`](error-log.md)     | `public, static` | `void` | <span data-ttu-id="1ef02-109">Заносит ошибку в журнал</span><span class="sxs-lookup"><span data-stu-id="1ef02-109">Logs an error</span></span> |
|[`info(source,message,scope)`](info-log.md)     | `public, static` | `void` | <span data-ttu-id="1ef02-110">Заносит в журнал информационное сообщение</span><span class="sxs-lookup"><span data-stu-id="1ef02-110">Logs an informational message</span></span> |
|[`verbose(source,message,scope)`](verbose-log.md)     | `public, static` | `void` | <span data-ttu-id="1ef02-111">Заносит в журнал подробное сообщение</span><span class="sxs-lookup"><span data-stu-id="1ef02-111">Logs a verbose message</span></span> |
|[`warn(source,message,scope)`](warn-log.md)     | `public, static` | `void` | <span data-ttu-id="1ef02-112">Заносит в журнал предупреждение</span><span class="sxs-lookup"><span data-stu-id="1ef02-112">Logs a warning</span></span> |

## <a name="sample"></a><span data-ttu-id="1ef02-113">Пример</span><span class="sxs-lookup"><span data-stu-id="1ef02-113">Sample</span></span>
```ts
import {
  Log
} from '@microsoft/sp-core-library';

// ...
Log.error("sample", new Error("error message"));
Log.info("sample", "informational message");
Log.warn("sample", "warning message");
Log.verbose("sample", "verbose message");
// ...
```
