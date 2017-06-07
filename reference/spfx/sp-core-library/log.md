# <a name="log-class"></a>Класс Log







Класс Log предоставляет статические методы для ведения журнала сообщений на различных уровнях (подробности, информация, предупреждение, ошибка) и с контекстной информацией. Контекстная информация помогает определить, какой компонент создал сообщения, делает сообщения полезными и позволяет фильтровать их.






## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`error(source,error,scope)`](error-log.md)     | `public, static` | `void` | Заносит ошибку в журнал |
|[`info(source,message,scope)`](info-log.md)     | `public, static` | `void` | Заносит в журнал информационное сообщение |
|[`verbose(source,message,scope)`](verbose-log.md)     | `public, static` | `void` | Заносит в журнал подробное сообщение |
|[`warn(source,message,scope)`](warn-log.md)     | `public, static` | `void` | Заносит в журнал предупреждение |

## <a name="sample"></a>Пример
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
